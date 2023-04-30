# April 29, 2023 TIL

---

# Table of Contents

<!-- vim-markdown-toc GFM -->

* [Basic Match Expansion](#basic-match-expansion)
  * [Static Matches](#static-matches)
    * [Multi-line expansions](#multi-line-expansions)
* [Dynamic Matches](#dynamic-matches)
* [Global Variables](#global-variables)
* [Word Triggers](#word-triggers)
* [Case propagation](#case-propagation)
      * [Multi-word capitalization](#multi-word-capitalization)
* [Cursor Hints](#cursor-hints)
      * [Things to keep in mind](#things-to-keep-in-mind)
* [Match Disambiguation](#match-disambiguation)
* [Search Labels](#search-labels)
* [Multiple triggers](#multiple-triggers)
* [Image Matches](#image-matches)
      * [Format remarks](#format-remarks)
  * [Path convention](#path-convention)
* [Nested Matches](#nested-matches)
* [Forms](#forms)

<!-- vim-markdown-toc -->

---

## [Basic Match Expansion](https://espanso.org/docs/matches/basics/)

In their most basic form, **Matches are pairs that associate a _trigger_ with a _replacement text_**.

### [Static Matches](https://espanso.org/docs/matches/basics/#static-matches)

For example, we can define a match that will expand every occurrence of `hello` with `world` while we are typing:

```yaml
  - trigger: "hello"
    replace: "world"
```

These expansions are simple text replacements and are considered _static_.

#### [Multi-line expansions](https://espanso.org/docs/matches/basics/#multi-line-expansions)

To replace the original text with a multi-line expansion, we can either use the `\n` line terminator character, such as:

```yaml
  - trigger: "hello"
    replace: "line1\nline2"
```

> Notice that when using `\n` as the line terminator character, quotes are needed.

Or values can span multiple lines using `|` or `>`. Spanning multiple lines using a _Literal Block Scalar_ `|` will include the newlines and any trailing spaces. Using a _Folded Block Scalar_ `>` will fold newlines to spaces; it’s used to make what would otherwise be a very long line easier to read and edit. In either case the indentation will be ignored. Examples are:

```yaml
  - trigger: "include newlines"
    replace: |
              exactly as you see
              will appear these three
              lines of poetry
```

```yaml
  - trigger: "fold newlines"
    replace: >
              this is really a
              single line of text
              despite appearances
```

> As you can see, no quotes are needed in this case.

There are a number of characters that are special (or reserved) and cannot be used as the first character of an unquoted scalar: ``' " [] {} > | * & ! % # ` @``

## [Dynamic Matches](https://espanso.org/docs/matches/basics/#dynamic-matches)

Static matches are suitable for many tasks, but can be problematic when we need an **expansion that changes dynamically**. For these situations, Espanso introduces the concepts of **variables** and **extensions**.

**Variables** can be used in the **replace** clause of a Match to include the _output_ of a dynamic component, the **extension**. To make things more clear, let's see an example:

We want to create a match that everytime we type `:now` gets expanded to include the current time, like:

Let's add the following match to your configuration, such as the `match/base.yml` file

$CONFIG/match/base.yml

```yaml
  - trigger: ":now"
    replace: "It's {{mytime}}"
    vars:
      - name: mytime
        type: date
        params:
          format: "%H:%M"
```

After a while, Espanso should pick up the new configuration.

At this point, everytime we type `:now`, we should see something like `It's 09:33` appear!

Let's analyze the match step by step:

```yaml
  - trigger: ":now"
```

In the first line we declare the trigger `:now`, that must be typed by the user to expand the match.

```yaml
    replace: "It's {{mytime}}"
```

In the second line, we declare the _replace text_ as usual, but this time we include the `mytime` **variable**, that will contain the output of the **extension** used below.

```yaml
    vars:
      - name: mytime
        type: date
```

In the following lines, we defined the `mytime` variable as type **date**. The type of a variable defines the **extension** that will be executed to calculate its value. In this case, we use the [Date Extension](https://espanso.org/docs/matches/extensions/#date-extension).

```yaml
        params:
          format: "%H:%M"
```

In the remaining lines we declared the **parameters** used by the extension, in this case the _date format_.



```
global_vars:  - name: "global1"    type: "shell"    params:      cmd: "echo global var"  - name: "greet"    type: "echo"    params:      echo: "Hey"
```

You can then use `global1` and `greet` in the following matches:

```
  - trigger: ":hello"    replace: "{{greet}} Jon"
```

Typing `:hello` will result in `Hey Jon` to be expanded.

## [Global Variables](https://espanso.org/docs/matches/basics/#global-variables)

_Global variables_ are variables that can be used across multiple matches. You can define them above your matches, and they will be available across all matches defined in that file and it's children.

For example, if you add the following into your `match/base.yml` file:

```yaml
global_vars:
  - name: "global1"
    type: "shell"
    params:
      cmd: "echo global var"
  - name: "greet"
    type: "echo"
    params:
      echo: "Hey"
```

You can then use `global1` and `greet` in the following matches:

```yaml
  - trigger: ":hello"
    replace: "{{greet}} Jon"
```

Typing `:hello` will result in `Hey Jon` to be expanded.

## [Word Triggers](https://espanso.org/docs/matches/basics/#word-triggers)

If you ever considered using Espanso as an **autocorrection tool for typos**, you may have experienced this problem:

Let's say you occasionally type `ther` instead of `there`. Before the introduction of _word triggers_, you could have used espanso like this:

```yaml
  - trigger: "ther"
    replace: "there"
```

This would correctly replace `ther` with `there`, but it would also expand `other` into `othere`, making it unusable.

With _word triggers_ you can now add the `word: true` property to a match, telling espanso to only trigger that match if surrounded by _word separators_ ( such as _spaces_, _commas_ and _newlines_). So in this case it becomes:

```yaml
  - trigger: "ther"
    replace: "there"
    word: true
```

At this point, espanso will only expand `ther` into `there` when used as a standalone word. For instance:

| Before                 | After                  |
|------------------------|------------------------|
| Is ther anyone else?   | Is there anyone else?  |
| I have other interests | I have other interests |

## [Case propagation](https://espanso.org/docs/matches/basics/#case-propagation)

Espanso also supports _case-propagation_, which makes it possible to expand a match preserving the trigger casing.

For example, imagine you want to speedup writing the word `although`. You can define a word match as:

```yaml
  - trigger: "alh"
    replace: "although"
    word: true
```

As of now, this trigger will only be able to be expanded to the **lowercase** `although`. If we now add `propagate_case: true` to the match:

```yaml
  - trigger: "alh"
    replace: "although"
    propagate_case: true
    word: true
```

we are now able to propagate the case style to the match:

-   If you write `alh`, the match will be expanded to `although`.
-   If you write `Alh`, the match will be expanded to `Although`.
-   If you write `ALH`, the match will be expanded to `ALTHOUGH`.

##### Multi-word capitalization

When using multi-word replacements, the default behavior is to only capitalize the first word. For example, the following match:

```yaml
  - trigger: ";ols"
    replace: "ordinary least squares"
    propagate_case: true
```

gets expanded to `Ordinary least squares` when typing `;Ols`.

If you want to **capitalize each word**, you can use the `uppercase_style: capitalize_words` option:

```yaml
  - trigger: ";ols"
    replace: "ordinary least squares"
    uppercase_style: "capitalize_words"
    propagate_case: true
```

In this case, typing `;Ols` gets expanded to `Ordinary Least Squares`.

## [Cursor Hints](https://espanso.org/docs/matches/basics/#cursor-hints)

Let's say you want to use espanso to expand some HTML code snippets, such as:

```yaml
  - trigger: ":div"
    replace: "<div></div>"
```

With this match, any time you type `:div` you get the `<div></div>` expansion, with the cursor at the end.

While being useful, this snippet would have been much more convenient if **the cursor was positioned between the tags**, such as `<div>|</div>`.

To solve this problem, Espanso supports _cursor hints_, a way to control the position of the cursor after the expansion.

Using them is very simple, just insert `$|$` where you want the cursor to be positioned, in this case:

```yaml
  - trigger: ":div"
    replace: "<div>$|$</div>"
```

If you now type `:div`, you get the `<div></div>` expansion, with the cursor between the tags!

##### Things to keep in mind

-   You can only define **one cursor hint** per match. Multiple hints will be ignored. If you need multiple hints, a decent replacement would be to use [Forms](https://espanso.org/docs/matches/basics/#forms).
-   This feature should be used with care in **multiline** expansions, as it may yield unexpected results when using it in code editors that support **auto indenting**. This is due to the way the feature is implemented: espanso simulates a series of `left arrow` key-presses to position the cursor in the correct position. This works perfectly in single line replacements or in non-autoindenting fields, but can be problematic in code editors, as they automatically insert indentations that modify the number of required presses in a way espanso is not capable to detect.

## [Match Disambiguation](https://espanso.org/docs/matches/basics/#match-disambiguation)

By defining the following match, Espanso will inject "Every moment is a fresh beginning." as soon as you type `:quote`

```yaml
  - trigger: ":quote"
    replace: "Every moment is a fresh beginning."
```

This mechanism works as long as you provide a unique trigger to each match, but what happens if multiple matches share the same trigger? In such cases, Espanso will use _match disambiguation_ to let you choose the appropriate one.

For example, let's expand the previous example by adding two more matches with `:quote` as trigger:

```yaml
  - trigger: ":quote"
    replace: "Every moment is a fresh beginning."
  - trigger: ":quote"
    replace: "Everything you can imagine is real."
  - trigger: ":quote"
    replace: "Whatever you do, do it well."
```

As you can see, all three matches share the same trigger. If you now type `:quote`, **Espanso will display a selection dialog to let you choose the desired one**:

![Match disambiguation](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAhUAAAF9CAIAAAA8yQ2DAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAB0vSURBVHhe7d0NdFTlncfxO4QXCSpUMSEUKGJCXQzhxZcicJaCiiSha8pysmcrK24PAVv3NGmFWm2qi2arCLrEPXZLQnvUg7unlEOjhyRIMdYuxldISLJsJUEpUEICWlBBwCSz9+WZO3cmd5KZPzOTIXw/h4PPc+c+z33JOc9vnufeoMfr9WoAAERogPovAACRID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAImI//3dgoICVQIA9C/l5eWqFAZJfqxbt05VAAD9xcqVKyPKD9avAAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEv3t989HPNmqSgCAQCd/kqZKbiL9/fN+mB/eJ65XFQCAj+ehP0U3P1i/AgBIXEL54fF4VAkAcMGYfwAAJMgPAIBEzJ+fd3V1vfbaa3/4wx8OHz5sHSucdaSkpKQxY8bMmTNn3rx5AwZEEHI9PD/XjxvpxQJAvxH15+exzY9Tp0499NBDTU1N9lHs8AhKkVChkpWV9fjjjw8fPlzVe0N+AICri+n9K33moYdHY2OjXlCbNM0ewfWCczR3lp305sXFxc4eAACJIIb5sXPnzoaGBmvod6ZFOGWbvkWPkJqaGlUHACSGGObHa6+9ZuWBmQt+1qeqbP7xdnV5u/S/vd5Ob1eH+mN86kN+AECiiWF+HDp0yAgBRwxYZefGDk37y9ypp3MzBy3OSPmn8V+/76szfjgy56fD7y5J/s4DA4ddae2lHTlyRJUAAIkhVvmhJ4T90GLIiKHnrrrKKtvhYRUGeL1XHD9x2VWDhl096Mprkr6SMmBk6oCUUVpamjdzunfsBGMffWe9K6sAAEgQMZx/6Izh3+v9StrQc//wd6evGWlngLXdKl/eeDjp9ZaOhvZzLaeSB3UmD+44XHe26X/Ov/Fy5/5GlTTWngCAxBHD/LDnH0Mv176Wee2JObeemPT1Lo/HTgM7RboOf/ppbfvp/Z8mD+pIHty56zdnt7/Ysf033o4vCQ8ASFDxmH94BnhGDDyT8be3fJY+ruWOv22/YeLnqSPPD0vuHDK4I3nouSuGnR82tCsp6YqRA/TwGNTV8fkpq51KDr3A+7sAkGhimB92AHR82TXSc3LI5UMzc+aljk/7PG3k4UnpB2bf+MG8Gfvn3NIy+6bmObd8MH/2ZZNHJg/qPPtJx4AB/uSwOwEAJJSYzz/0vz8/fm7c4E+8588PGjxwwi2Tb82/Y8YdN0654auTxg7PuGbI1y73piWdG3r61PCBpy8b0HGqvWtAUkByOMsAgAQR8/mH/nf7oc/GDz112ekTAzvOJnWeG9h57soRQ786ITV98pjJN427Zeb4b8699tvfui71uus/Oz3siGfElwMH2m2tAgAg0cRj/qF1eFvePzbvKwe6Pm5POnfajJCzA7uMILH/DO46O2zY4EFXT/gyaeSnV11utbWaq04AAIkktvmhM0PA++ZvD0wYfvrboz8Yfbq5q/UvZ9uOf3nixJcff3L2+Men2z4+feyEXj174mTHqU/HXDM4ddxQOzGM5uQHACSeuMw/NK11/8maTX8aN+LM39/QWjjjg/unNi2d1PjPmXv/5aa6h+e896/z3/np/HfunvbevGvrJyS3jBs72MoNqy0AIAHFZf6hJ4FH2/WbD/97zf+ebD8z0NN55dDzo4Z/kTbizNWXnz1/+tze985/0Nz1RafniuRzw0/+OTfrzx3njfBQbQEAiSdO8w+r0PTH44/fU//E9/6vrORI2b+1PfXjE8vyPl76rc9+/tMv361LOnV20OGjg39WfMXahzqTBvnDwy4AABJHDPOj++ivFzya9+iHZ+v++Om7r3/etPvc6U+7Bg3SOjq8o8doyYM7Ww8Z1YED/WnhbA4ASBwxn39Yo79dsMpW4brZl+f86Op/fPjK7z029Ot/40ke1JmV1fXMcx0/e7xzaHLAP5joLAMAEkEM88P+/5Yb0RGYIlahff+ZMdclpU8acH2m58rkzqGDOq+6SrshS5v9Te+UaQH7R/S/QAcAxEEMx+WxY8eqkskOA+tv3afHOn731PH6mi/erzm/69WOHdu8la9oVa9ov/utZ/d7/v8dur7/mDFjVAUAkBhilR8ej+e2227T/1Z1HzNEFL3a9lHnyxu/ePE/zv/n013PPDngmScG6H//Yv2Ac2f9eaN3Mnfu3O5dAQD6UAznH3fccUdmZqbruG9lg8Ws61vsjf5PzX21G264QY8iqwwASBAxzI8hQ4Y8+eSTeoSoejcqJUxqk2+jqpjhUVJSonel6gCAxOBxDtbhKCgoWLdunaqE4cyZM1VVVW+88caRI0c6OjrUVgd7guKcqQwcOHDMmDFz5sxZsGBBcnKy2hqGEU+2ep+4XlUC6f1HerEA0G94HvrTyZ+kqYqblStXlpeXq0oYYp4fOv0Q58+fj/RA+nA/ePBg1+WvHpAfAOAq6vkRj/di9YF7yJAhl0VIbxJpePSM8ACAKIpHfgAA+h/yAwAgQX4AACTi8fw8nkY82apKAIBAF9/7VwCAxJeI718BAPof8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACcnvn9+ZfZeqAAD6i1erX475v1+i58fiRQtVHQBw8duydVv88uOlxi61CQBw0bp7svEgQ5AfPP8AAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuRHHGz/dVbSr3epygXZdd+SrKQl9zzbpuqR0s9k9vZDquKm1x3CIbje6N0ioN9q2rfxmYMnVSURxDo/jHHBGPLUnwsfmxJZqMF3wXcbOr87W1UuwIHtZeXzftG56cUfpKotiUlwvdG6RUD/cfz1Va+/3qQqASIKEn3nVe/Wt6taVMVh/nHrkm2dmxqsP7sWjFNbEbnmo/W3juYGApeCk6999NdpqX9tOK7qvWo/uPW/gnY+U//M6xsbkm9KU/Vo64P1q72PJa3edEBVdt3nW405sP2eoDmK+XV+17Or9Y33PLvdvZXNsbO1EmIt9QSuiuiHtjY6mofTsMdzs/Y8pJdza7S3Ni1MWvLYdmsnH8e8xNf5kqz79pobAvg/DThtk96Js3/HCYS8gSEOZ5yqsdF/P4P4dgg8Sbf+Hbd09aZnfZdpX2+3u2QIvTFkE4PbgYB+68zBvdqE28dPOPZR0NTh5GvvbnyhTWv9aEuo2Ylf8tQfzV32nRRVi74+yI8p8wqaP2y2yntryjPm56Yao8PETemVxhxlW/47xfbg/tamMu0+feOLP1jg1iqQb+dfFNR8P2lJTZ7Rm1FWg2DbptlrW/79aWMa1Lkq/YcP+Ef5Xhr2cm7WnuN+8GhD5TxrsvXIArVLsO2//r62yjyBTQ2/nKI22g5sr5lknZ7z6D4Lvhvcv//mhLiBrofzn3bzU2sDD2Hx7dDQ+fSPm9b6gtb1Jjhv6X3a5hpzY6DAu9TTRpvLp2EcCOhP2ts/1FLGpySPn6J92HhGbTSNuO2WZUtTtbRrF6+dOzdTbewjccgP8yuz+c1RfZ+dnTdvS4U5LmzfvaUgb8l1ZuHWJfeaw+K43G9om+vUt8tbl5T41vr9rQ60tlitgvh21vfUy1ZvRrmp1fxiW/mUZvc25ZFKX2+6Xhr2cm7+PcPRw57XLXjEcbG99+m4OSFPsnsnvZ62v9vUJcXz6q2uXPsPuKXGzmYhkOvhej6H7p+GcyCgHznZ2K5NSRmhp8XkFG1ve4+POsxFqlWvb1z70Sd1TUYhVk87uovz8w/rW/CCGxeX796labsqahbn+b8Xq5iZuKlebQrka3Wo8p10u1VEMtMCHh64jp6uej23MOlziOKjZlfdlqcM+rdsX9DmRv4Vu/tJ9nK4MGSMnqpKIW5C0C2NnbgdCOh75uLV5GSjmJIyQWs/2FMemItUa+cuW3XtVdMyjcLaW6bGbskqQB+sX+mmzCuoqdnedrBp3jzzK62h98fsqtUfN4/1t4pIUGCEPyRF8RUA40WjTQ2V2ve7reDvuu+BHflq/cpYqoqU60mGPlxYmo/W23fJtf/wM/gCxe1AQJ9rOvh+6+n315qzilXvGOWdYT9Fj6u+yQ9jaWJLyS93ZN6oXtnU5xZvbXo+6LFzN3qrlopKf6uImIfwLdzvfSzXMfXpWXjnFhn9e/1bR0MPiG2bSiKcf/R8kr0cLpC/H8ddcu0/YKOxs1WKvlAHsp+6A/3IwYa2qxZ8w5xJ+CYWdccPqg8TSpyff9gLKcaI0OxYhjIfSOSq3YLfrbItuDG9vEa4eKUfwnxsbh7CeBgb8il3sPDOTbcg98eacbHB71/Z9PHOug8T35m/P/jXHWavWqKp0/ullh/p/MPtJHs8XEi3LplQYfXjvEuuN2HKI/uXtKiNu+cJ5kzhituBgD53/KO6YWrxypKSMiGt7SPnq1aZ42/Sur1/lTJ+0XeuUeU48Xi9XlUMT0FBwZ3Zdy1etPClxi61KY72PqYPH/yiWUI69OzqhfvyXN4ri7a4HQi4NNw92ZhIbNm67dXql8vLy62N4eij9SuZQ89WbCkQLV4h1g5sL/5hc7hLghcibgcC0IuLJj+MXx9buPkb2/jWmUD8v4+ZZf52SNhLgpGK24EAhO8iW78CAETXpbF+BQBIGOQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAQv7vl6g6AODix79fAgCIE/IDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASPSb/Khe4ZlV2qIqPvpGz4pqVekvYnRRF9htrG+1688XuKQ0bixcV9WmKokg1vlhDCsO0R0Ceh1Tsjd4vRuyVaW/iNFFXWC3/fJWA32p7sUHlr3YqCoBwg2SYzvWLSt8wPzzUp3aFk1xmH/MXN/s9XmzMF1tBQCE1LbzldbpM1obwh7326vWBIVE47Zjd24sfVr/U5Lb+px7FF2QPli/Cpg1+CstpbOC5ijmZ9Xm5lmlpUGtDDllWm1RhmPdpFn14dvT7t3RVeAyi+qp2xEsdvugit3K/ePAdk52Q/WxvyP7rMy2bqfqY3febU9fb/5WLv0b7M2Oqw7drdL9B+RkN3cetPvpOzpXu7t16+/BpQvgUnBsb7027Y6F01pf2dGuNlnadq4ufP5trXXrz0PNTmyTl90z2SqNmjJ1bGvbMasSPX2QH9l5y2v3NVvl6oqymfm5+pykekVGUWaVMUVpzt+81B5JaotKtBfMeUthUCtjUlO13JrcqHUT385Vy2uL1nYbdvyfluWoQUkfunKa1OzoBW1zmbnRyfVUna2qMosywh7hHA2biyeaGyomWf04z8r1VENw7unxVOQFduXef69X7XoCIX5A3VWvyNHM/XSuC1q+zs25qFu3oW4LcOlo31On3TwlRR/3tbqGgHE/9fZHS++doaUtevjpjb546F1b2+G01FGqEjVxyA9ziqCYY4E+KpdVmIOCPiYvLzaHESMRVpmjTXpuvra5Uo1PM9e/4Fvx8rdq2d9ktQri21nfU2vaHzzCdf+0em2RZvefXli83CwEcDloQKvsDfoIZ+3QK2fD9Oxs/b/phRtUP4Hn3POFODn39N1AfyvX/sO4ard7FeIH5Cq8cza4dhvqtgCXjLaG97Sp01P1tMi6Wavf0+OjDt9DjjVbj+55znzasbr7lOVX2v3hh03Y4vz8w/pCqo8K5qBrxEeeuUVnx0xGUa3aFMjXqqVyc6bd6gJlTvSNZCG4HjSoVfgDXPDh7LUbcy0u+kL03+tVu+r1B2TJ3uAt3mfuGd7EwaXbWN8WIMGZi1dZ5nQhZfo07b29gXkQaNT8leZDjgcXjZ5+v/m049H5KeozK12e11aU3j1NbYimPli/0lmjsvGV3h8EvT9mV62iGB9hDP1uBw1qFf5wHNiwekXG5nzfRVe5zQMuTMj+Zd/ow38PwngXSz+iluP6pCRIt25jfVuARNe4rbL1cOUa69WpYqP8e9nbU3p4bNDu2fjg7VFfubL0TX6Yo3LJUv+YrNfdnlkE0fdqqlgbtfgIOGj1ihBfdYMParbyPQAwWqkMzJg0s9Zaf2kpLXHrynm4lurqgJE1RJOocfQf3lUHC2gVHuOG+B4ehdJLt263xfGgHuiXGhreHp1dYs4kfBOLPbsb1IcRaNu54didzrlI1MX5+Ye9pmEMHLWOIDAfJOSonUKOD9l5mWVl/lbZq9ZrRufSJ6zZG5rXN6mDVuSF+qobdFDj27Xx2NxsZTyIVg+JjUcJ1qUu1fJdu3IcLqNCS7dPXxeqyQUJ0X94Vx0svB+Qzn53yphF9PobIS7dxvq2AImtrn7PWLV4ZUmZPi3t7Xrnq1aTF+Zq3d6/Ssl5MHCRqq3t8O7nrUmM+Sf6v3vo8Xq9qhiegoKCO7PvWrxooarHlz44VeTF5vfUWkpnZewrdus7hgftc6GvGsAlZcvWba9Wv1xeXq7qYeij9SsZYznD8cQkmlpKlxbVuvYdw4P2udBXDQC9uWjyw1gWCWtFJAL2Uovx8k9mVfdv4bE4aJ/r9aoBIBwXTX6Y7/RE+Z8/sd4TUtyG0VgctM/1etUAEI6Lav0KAJAwyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQSIT8qF7hmVXaoir9V1QuM6JO9J09K6pVJRrso18iPzIgoTRuLFxX1aYqiSC2+RE0zLSUzgqo6x9HNrwxbEUke4PXuyFbL3DfgItP3YsPLHuxUVUChBskRg+F5p81O4+pbdEU2/zIzlteu7nSN3C1VG7WZmr7mlVVq64omzkpQ1UAALa2na+0Tp/R2lCn6r1qr1rzUuDO7a2j7t1Y+rT+5/606mL3KLogMV6/MgLEDozmfVp+fmZZhZpyGPGRn5tuVbRmfW5i8H9P1r80+xizFGPyklOm1RZl2IsyxiaTahTwNdtfCd5NfVZtbvY3MITowSgqrh8HtnOyG84q3a82mdw6DEnaiXlWxmUG3TdF/9i3wdzT6kK/WyFuL4C4Oba3Xpt2x8Jpra/saFebLG07Vxc+/7bWuvXnoWYntpSc+ZOt0rSp061CdMX6+UfGpJm+wKiuaMrPLcxb3rTfHI1a9jf546O2qER7wev1Vi2vLVpr7t5SWjGpWd9ibizLWVGdXvimXtJmrte3qkWZjKLMKmOH5vzNS40hzplWdjp1383kO+Kbhb4EM7j2oI+jOU3GYXVVmUUZgaNwD5wNX9A2l6nNkXV4oZ1kBN83m36x6mfTsl+fGFoTRWOSaE4KQ9w3AHHQvqdOu3lKyqgpU7W6hoClp9TbHy29d4aWtujhpzfeo+KhV3X1e2ZMDXfn8MU6P9Jz82dagaEPx5kT0/VAsQYqfZyqNeqWmetfMMdxfUjTrN3TCzf4Rnb/RidjeF+/yhwQ9YNYnfpHRP3T5cVGB267GXxHDOIcU5tUD2uLNHvn7A16mvlmUL0IaJheWLzcLETYYVQ6CUEPd/O+GpmRn2+tLBqTRDN2Q9w3ALHX1vCeNnV6qp4WWTdr9Xt6fNRxbMc68yHHmq1H9zxnPu1YbU9ZGl6ynn/snvr0siy1LYpinR/24GMMx3n6cOSrN++rNesh6d+vzcUTXY79pTuQuSZjyCiqtbb4hn8jPuzeu+/WA18P+piaaffgDzpT9zALJaihLaIOo9KJG/WzMC+1cKK5sqjfOLvbiO4bgKgxF6+yRhnFlOnTtPf2Bi5hBRo1f6X5kOPBRaOn328+7Xh0for6LOtu6/nHjfUxeYQe8/xQg1S1PRynT8ys3dccMMC7qF6RsTnfWpwxFrDU1iDmmoyi1qGs4d8XVhaX3XqgenDGR/DQHGpA7y7UmB5Rh1HpxJX1s2jeZ1yqft1N+6udNy6y+wYgShq3VbYerlxjTR2KjfLvw36K7m7aPffOONrWqmpRE/v8MAepzSVqVV1nDNAlJU1hv3rVUlriNv/Qu/E9K3Eye1/qH/xD7NYDYyCtWBvUg+8BQPWKHF/wZUyaqV4uC+cMjYZWKWSHrqLSSUh6L036z8L8UWTnZRblFPkuO+C4oTkevAOIioaGt0dnl5jzBt/EYs/uBvVhBNp2VvlaHdvx6tujU9NULWrikB/mUFRrraq71t1kr1qvqeWTpVq+b/7h22o+KzYX/XPMXZyvCJm9O+YOIXbrgT6QlpUF9GA+oDY7MB5Zq6fQxsMIa4nHcYYBsjc0r29Sh67I88+i3DtsKZ3ldnqRdeIu4L4F0K/V/lHogaj5Uz3y+wYgCurq94xVi1eWlOnT0t6ud75qNXlhrtbt/auUnAfvnqbKptTUo78yf/lDn8TUTS158HZHn9Hh8Xq9qhiegoKCO7PvWrxooar3R/qX6oq8oJeVYq96xaz9q1gnAtAntmzd9mr1y+Xl5aoehnjMPy4yxmqUaDHowpivNxMeAC4a5EcAfebhMR7cx3vuocvewNwDwMWE/Ahg/ItRvGsEAGEgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABIkB8AAAnyAwAgQX4AACTIDwCABPkBAJAgPwAAEuQHAECC/AAASJAfAAAJ8gMAIEF+AAAkyA8AgITH6/WqYngKCgruzL5LVQAA/cWr1S+Xl5erShgk+aFKAID+Jbb5AQCAjucfAAAJ8gMAIEF+AAAkyA8AgAT5AQCQID8AABLkBwBAgvwAAEiQHwAACfIDACBBfgAAJMgPAIAE+QEAkCA/AAAS5AcAQIL8AABETtP+H1bJ9EOGJvNXAAAAAElFTkSuQmCC)

This feature is particularly useful when multiple choices are needed for the same trigger. For example, you might define multiple snippets for your signatures and then use match disambiguation to choose between them:

```yaml
  - trigger: ":sig"
    replace: |
      Best Regards,
      John
  - trigger: ":sig"
    replace: |
      All the best,
      John
```

## [Search Labels](https://espanso.org/docs/matches/basics/#search-labels)

When using the Search Bar, matches are displayed with their replacement text as description by default. While this works for basic use-cases, the resulting description might become less intuitive as you start including variables.

For example, given these two matches:

```yaml
  - trigger: ":tomorrow"
    replace: "{{mytime}}"
    vars:
      - name: mytime
        type: date
        params:
          format: "%v"
          offset: 86400

  - trigger: ":yesterday"
    replace: "{{mytime}}"
    vars:
      - name: mytime
        type: date
        params:
          format: "%v"
          offset: -86400
```

the Search bar would display them with `{{mytime}}` as description, which might not be very intuitive:

![Matches being displayed in the Search Bar without label](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfwAAACpCAYAAADOZo/jAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAABiySURBVHhe7d0LdFXVgcbxL+ENKtQiDwsUMbEuDC+1PhKmFKxKEjul6mLWqo52uiBx2llNOhVb20xnrJn6gNqks9opgelSF51pKWOxQxLqKFYHYn0CIcNUEhWBGhLQAgryCLmz93ncnHtzL3ldYpLz/7mOOfucc/d9JOt8e++zzyUtYggAAAxo6d5PAAAwgBH4AACEAIEPAEAIxFzDX7p0qbcGAAD6u1WrVnlrCQJ/xYoVXgkAAPRXd999d0zgM6QPAEAIEPgAAIQAgQ8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIQAgQ8AQAgM+G/aG/Ngo7cGAED/d+jbE721M4v/pr1QBH7kgUu9EgAA/VfavX/sduAzpA8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIRASm/La21t1TPPPKPf//732rt3r/yq09LSnJ+dNWjQIE2aNEnz5s3TggULlJ7e/XYJt+UBAAaKntyWl7LAP3z4sO69917V1dVFg94Khn2i4O+oMTBz5kzdf//9Gj16tLelawh8AMBA8ZHfh2979jbsd+zY4awHBcPfrgfLVnw5nq2zpKSkXb0AAKDzUhL4Tz/9tGpra6OhHB/sXS0H2e029Ddt2uRtCYHqQmfkI6e8wdsAAEDPpCTw7XV7P7D98A4uvmjZWyKmgRBptT/Ncjqi1pa2Jfg4K1SBDwBAiqUk8Pfs2dMW5gF+OX5fi1n+NH+2juZnacitmRr311P1qbs+oWu+MVZ53x2t20pH6kvfHKxR57nHW/v27fPWBo7q8kLl5JSrXT8+d6XzeW0pyvA2AADQMz0OfBtMwevrw8aM0Inzz/dKsWHvr6eb5dwDBzX8/CEa9fEhOu+CQfrYuHSNHZ+ucROkiRMjyro8osnT2h5rn8NfHxgatGtthWq8EgAAZ1NKeviWH+Yfm2gC/6/+UkcvGBsT0P5+3zk79mrQsw1qqW3WiYbDGjnktEYObdHercdV9z8n9dyTp7VrR1tDAQAAdF9KAj/Ywx9xjvTJrIt0cN61Ojj9U2pNS1MwroPB37r3iI7UNOvoriMm8FtM4J/W5l8d18bHW7TxVxG1nOrFsPcmyhVWm763Wc8x67aclpbjbHM0VKswx9+eppzC2OH46kL3+MRz7cxj7eNyylXuHJepYtu9rylWpl+f/8DAa4lKwesLcuoIHJuWU6jqZAcDAPq9lPfw09LTNGbwMWV+5iq9nzFFDdd/Rs2XXaIPxo/VyVEjdXrYULWMHKET544y5RFqHTRI545Nd8J+SGuLPjjs1hMMervea7flrS/UnaXS4qoqVZUVKFs1qsgzIV5drpzMPNVllamqqkwF2WZPhQnrQCrnLiow/6/R2soEyVm9XhXmR0FJkfKXmbqdOsyG7AKV2ecyS0l+J67Z9+D1+RrKc5SZ57wa97mdeiqUl5mssQIA6O9SEvjBcG451aqxaYc07JwRyspboPFTJ+qDiWO1d3qG3ph7hV5fcI12zbtKDXOvVL35+foNczV8xlhnSP/4ey1KT48N+mDdvaHC5GDJlpUqys1VbtFKbalyQ7w4r1gqq9eWlUXKzS3Syi2PqcwGdkVpW0jmLjIRao5eW9muZ1293g3YRblSRoapOzdf050905Vvn8suncj7Hr0+y/TsM4trVFBljg3Ws6XKvDpTz53JRwUAAP1XSnv41gcHTmjK0PcUOXlSQ4YO1rSrZujaxdfrmuuv0KzLPqHpk0cr84Jh+uQ5EU0cdEIjjh7W6MFHNTy9RYebW5U+qH3Q92bwZ5ctk8nkNl6I27AuiZk1n6H8xTZRa7Sz3t1iDtYym7I1axXbya+Wm/eLYuvuhp69Pq/hkV2mZe1aF7lyByh2KnA4AGCASGkP3/5s3vO+po44rOFHD2pwy3ENOn1Cg81y3pgR+sS08cqYMUkzrpyiq7Kn6rPzL9IXP3+xxl98qd4/Okr70sbo1ODBMfX1VtD7si6JD8JMTbe5mT3drMXKuCTLW2uTkb/YGWaPGdb3h/Nt976Hevb6vIZHYN5AcHFG+VWnXXTxAWDASXkPXy0RNbyyXws+9oZa323WoBNHvdA/rsGtbvgHl6GtxzVq1FAN+fg0nRo0VkfOP8epJhj2vR36PZKRL9uxDg7rt/WqvQ0fNfNa7JyBxEuJOjOVAADQv6Qs8C0npM1/W379hqaNPqovXvi6Ljxar9bGP+l40wGdOnhQp959T8cPvKujTWbZb8pm2/GDh9Ry+IgmXTBU46eMSDqrv3/whtKjw/purzp7cb7Z03dk+vMGEizkPQAMPKnv4RuNuw5p05o/asqYY7rlskYVXfO6vja7TndO36G/ydquv7tyq74z72X90w0v6rtmuW3Oy1pw0TZNG9mgKZOH2sr6WcjHihnWd4bzs7W4T3SbveF/rtMDQOikvodvgzpN2vyrN/UfD/2vDjUf0+C00zpvxElNGP2hJppGwMfPOa6TR09o+8sn9Xp9qz48naZzR57Q6ENvK3/m22o56YZ9tL7+JqNIJQXusH65271PPkzeq+HrT+SrUF6C2/XUUK7yBJsBAP3fWenh++t1zx/Q/Xds0wN/+3+qKN2nin9u0sP3HNSSRe/qzs+/rx9895Re2jpIh48P0d53huofSs7V8ntPa9CQ2LAPrvcXzj35NcUqNnlv771vn/eB8M0pV3W1DduzP1suo8i/XS/P+bKdcpPw9rkLc3KUllmsne5hAIABJiWBnyyY7br9nr133jyurc8f0UvPfqC6V0/o6JFWDTGh3tIS0YWT5HzpTuMed9vgwbHBHl9nvxG4XS7Z5HwnfO2375iGQV5esdbu8nacVRkq2lLvftlOTYWKi/Oc57YT9O29+Sv7ysRCAEBKpZkwjabp0qVLtWLFCq/UOfbht9xyi95++22nbG/v8iVav/gvztWlVw3T6OGnnGXmjFZNGH1SLcda1LhPeu/dNK14IF3Hjrq3ivmmTJmiX/7ylzHbOmPMg42KPHCpV+pN9qt081RRUKUIKQoASIG0e/+oQ9+e6JXO7O6779aqVau8Uop6+OnpbdUEe+SJ1pt3HdOkiwcpY3q6Ls1K03kjT2vEkNOy/8DeZTOluZ+NaNac9o8PPke/4E3WK+sz9+IBAMIsJSk6efJkb61NMKz9n9aR/S36zcMHtG3Th3pl00lt/l2LntoQUeVvpSqz/ObXaXr15dhevH38pEmTvFJ/0KDy0g4m6wEA0It6HPh2iP26665LOtTuB7+/WE1vndaTqz/U4/9yUv/6w1Y98mC6HnnALObnT8vSdeJ4bIPB1j1//vwuD+f3toZyOwnOToCz/xKe6d0/lmiyHgAAvS8lPfzrr79eWVlZZwzkYOj7QW6/Yceutm2PPc532WWXOY2Kvq9OxcV2AlyByuq3KOar7QEA+AilJPCHDRumBx980An9jgQDPRjqVqJtNuxLS0ud5+jrMoq2uO/B/it0hD0AoA/p8Sz9oGPHjjnfx/7cc89p3759amlp8fa0FxwNiB8ZGDx4sHPNft68eVq4cKFGjhzp7em6j26WPgAAqdWTWfopDXzLVnfy5Ml2PfWuso2AoUOH9vi6PYEPABgoPvLb8oJsQNvh9+HDh/dosXX0NOwBAIAr5YEPAAD6HgIfAIAQIPABAAgBAh8AgBAg8AEACIGU35bX19jb8gAAGCj6zH34AADgo3fW78MHAAB9D4EPAEAIEPgAAIQAgQ8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIRAu2/auzH3C14JAAD0V7+rfvLMX61rA//Wm2/ytgAAgP5m3RMbOh/4v9jR6m0FAAD9wW0z3Cv1iQKfa/gAAIQAgQ8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIQAgQ8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIQAgQ8AQAgQ+AAAhEA/D/yN+vnMQfr5Zq8IAECfUKedqx/R7kNesQ9IeeA3rZmr22fepe1Jyj1jA36uNu7xilqor9Se1lfmesUecxsQ9615I0kZAGC553Y6XNaBZ5fp2WfrvFIiPQl/+9hlemlbs1fuvhQH/kZVPizdvuFnmpWw3NeZBsSGH0kPL/caKPFlAIC1/80XvLWQO/SM3vrzHI3/c60OeJu6plm7n/j3hI89tu0RPbu6ViOvnOht6ZmzMKSfpYlTvFWHX/Z655t/rPtMqzDaMtx8l7MebClu/35crzp6TL426QWtucmsf3+j2RHs8Xe+ftcb2niHu/324KjBlEs02Vt1xJcBIGyi51F7rnTPncvXubs2fdVsv+PHanJK7qiof86NGd3d452b7bEx9Zl9Sc/Tnatvo8kMZ1+ibc7ByeuxedOWAX4u+GXvcdH3196x3aamaZ/T1Gn79VaiXrhpELy0+jHz+Ea9ta6jkYBYI2f/veYv+ZLGeeWe6uVr+CasK6S7ak9rzU+Xun8omxZpTbTs/hJmLViq+jfr3YcY2zetUuY9u8xxlVqga3X7BnP89xZ6e4M6V7+1/fuXaE1Gpbtvw2K9WJL8FwoA6IgNR9spC1ql5cGQdqzVz766yls35+ySubovWrYNiGBId6K+bd/QGq/xERWz7cz1TJh2rfn/C3rHCfh6vbPN/nxBLz5vOp17dmmvKWXekK/xdnM7zWp+Uxo3dZxGTp0lvblDx7w9UWOu01VL7jSPn6iLbl2u+fOzvB29L7WB7304UfFlG9alX3c/uLmL3PD+shfcTrlOjfZDt+vr1nu/1DfU2LBUi26/2CmdWSfrN38Ar64L7JuSr6vNH+FWZ5/lH+eLLwNAiMz9mds5qt2shVMu1sLHT2vZre6uBT812x//urSm1A3V2T/SD51jd+n22XbDKr0a7LWbQL3adto2/EiZwbLToWvT1Nn6/E5gbfDScdu2CR3UM/4zi53XsXe3CfjN682x1yrT7Hc6nXt2miaANHlqkvw5tMNE/iyNG2PWx8wwPfHtau7kdXp3uN70+Fcv11vvbVWds56aa/XJpDDwTSvqpp1aFP3Q48tdsVBX3Or9UvdU6sWMRWdhDoB3acAZ3jG9fadVZ9mJgCV65ya/FRlfBgAk09YbvlhzbrC9Zy9MfbMXa469zBu9XBp/GThWp+sLSrAtaT3e66h/qlLbd9c5j706w2xo2OWWtVRXJJkY7g7nz9BIpzRO46aZPv/uzgW2O1xvevxLlumi8+coy1lfrqtmp2oAv70UBr6d4DZd66PDLfHlrrHD+ps2bVTT82s1eUGi4fue8luA/mJbrna7Hf4p1YWBiYexZQBAMm2XY9/Q1qfciX1Je8idkKr6ktdjO5jmx7a1Wm+224bBHDvM75U1e7omOEfHq9PuVxp19JXlXk99mV50yk93c/Le2ZfaIf1oi80TX+4KOwTfsF6VT2UlbV11n/0Fmx7+o3biXyLJJh4CQAjFT7IL8Cft6fYSd0h+XX7cyGnyHvKZjE9RfZ2px7+OX2+220aAO8zvlpNev99dq6bzF+pqr2fe1lvfqgO7vWP6mF6etNcVJpQzVmlTzHD+QuXfo8As/e6b9b1KLYj+AZjlDLMwAQCxZn3ZuwYfZS9/xl6Ht6G6rFuXda1U1ddxPf51/GgjINBZTTaacOCtrRoVHc732WH9iWp6K34mfpamXqkks/THaerNX9IFXulsSosY3rqWLl2qG3O/oFtvvkm/2NHqbe0Kf/g7fnjcL3eNvV3i1QWp/GKdTrC3dQTnHsSXAQDoo26b4fbj1z2xQb+rflKrVrXdAZHiHr7fA2+7jh9b7gITtOvXdW8oqPvsRMNvSPcs88I9vgwAQP+U4h5+atie/XJ721w3RwYAAAijXuzhp8as7wVnzQMAgJ7qw5P2AABAqhD4AACEAIEPAEAIEPgAAIQAgQ8AQAgQ+AAAhACBDwBACBD4AACEAIEPAEAIEPgAAIRA0u/SBwAA/VO/+S59AACQWgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACHQzwO/WoVpaSqs9ooAAMRoUHlOmtLSclTe4G3qFTu0umiFqpq8Yh+Q8sBvKM8xH2yhieLE5Z6xAR/8peVqZSSilblescfcBkRO9AniywCAs8nNjP7Vkdv6+De15PEdXimR7oX//qdWaEmRqdtZfqGt3vbuSnHgV2t5sVRWv9JEcaJyX2caEPVlUvFy88oTlQEAZ1P9zhpvrZ9oelq/bbxc1zTWdjOQm1X1UKIw36EN+2/U6vIfOktpfqN+csZGRcfOwpB+li7J8FYdftnrnVeXK8e03qItuOpCZz3YoqsujOtVR4/JU4VqVJxp1t0HB3r8na/f5Q/z2CUwapBxiXnFAfFlAAir6PnUnjPbzqFt51Z3VDQtp9ycYQNlfwmchO15PrrdLIXVbn15Fe7+ijyzvaN6GrzzvTmu3KnPG032tzvHVjqHtgme+93Fra4z76e9/du3SXOu101zGvXbp5q9rQGmQXBf0aP6gxr1xA86GgkImqEld8zw1qUJs2ZrcmOT9nvl7ujla/gmrEulxyIRRaoK3F/o+kWKRMvuLyt3UYFqdta7DzGq11cou6zeHFelAmWrrN4cn3Acv3P1W9WFmSrOqnL31S/W2juT/0IBAPEylL8421mrWO+dWavXm06ZlL043+y1YWk7aQEVeW5nzjQc/GDv2Bnq8dUUq9g/wIZ9ZrFJA0+F2RczaFCv+EGEijzbgOno/STSrNdM1/zTs8Y5gaytte0Defzn9I/lX9Y1mqibv2N664EQ75KmJu2dOF4TvGJ3pDbwG3apzlt1xJdtWD9W5H5wuYvc8F7mBbdTrtMu+zu06xXrvXBu0K66ApUUJf64Y3WyflPz+orAvox8mchXZfTvxz/OF18GgBDKXel2kiJbZE/JGUUl5rxqeOdr2zmz5+HF+Rkmd0vdkC7wO1ZlZo/J5rWVqt7lJ0OBqpz67FysDBVticj0zdw9VWb7liLpDPW0nZbN+dx2BCMrlVm51g17/3inoxjkzv1y9/nPVyPbxzzT+0moqVYva7YuH2/Wx8/Up7VNr3XyOn3b9fmH9MQ7r+kn3rX6+5KNEvyb9LXuNhY8KQx80wrL3KkS84G7MRpf7opcLSqokNPIaqjU2qxF3aijI96lAWdIx/T2oy0++8dQop2Z/mhAfBkA4LLnavvTnq9tR8qsZi9WTD6a3rhzng30ujP9YDWPy3POwYHLqskkqCcq/jmN7OmZ3lqmprsdd1dwuN8ssSMNnXg/Ae5w/kyv1z1Ol8+RXt6eILATmHDD3d71+W/p5gsv19e8a/X/eMM47wiX0zB4VCosv02m+h5JYeDbCW7TVRqdkR9f7ho7rG+HVRpMay1rUerj3rba3Bahv7gtVqehklaq6YGJh7FlAIAvd5nb464rdXviBSXeKKsv2tP2FtNrz7D54JX9Hnbx8g6SImE9yUUvC9tOY6CFUL3cbTA4IwiRepUFGwNGh+8naoc2VDZqb+VDXk/9mypxyv/d49n0Phv2K3WHVn/rcz0ayveldkg/lRPe7BB83XotX5ul1Oe9bcWd6Q8s2cRDAAixmEl73jZ7SdQkZE2NE6PR83VG/mInOKM9c2+xE+L8W+/s4vew23rkLn/Sns5QTyLtnjduRCDT6+479ceM7nqSvJ92amv1hwtzVer1zNt666/p1VrvmJ5oelor99/YrsffE708aa8rTChnVagiZjg/V6bxFZil3325K6tUEPwDOsMsTABAMm2T3VQQOF9nFGmLd729Q6b3vsWbp+X3sKO6Uo9ljn8s0G3PLquK6cVHr9Nb5nn9OQNtkryfOFu3vabJ0eF8nx3Wn6g/bIufiT9DN+UrySz9ccr7VoLhejtJ79VHo6MH7tLDL/KJBCxZsiTy6//8L6/UHVWRAmVHyuq9Yrty15hfRKSgyiv0lvqySLYKzCv3xJcBAAH1EROoERsnvX6+PisGxvuxWW4zPSjFPXy/B952HT+23AUN5SqtOMNwyllhJxrabwpa5rXq4ssAAJ97L703LJ5dJv/Gp/5qoL2feCkf0s8o2iJ7a4T/OcWXO8P50DPXanGvT5RzJ5L4Q0vtywCA9gpU1cEkuv5loL0fV5+8hp+70s6e9GfNAwD6IvdcbZeBcRfTQHs/8frwpD0AAJAqBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAQAgQ+AAAhQOADABACBD4AACFA4AMAEAIEPgAAIUDgAwAw4En/D02BZ1JHBhVRAAAAAElFTkSuQmCC)

For this reason, Espanso supports the `label` match field to override the default description, making the search UI more intuitive. For example, adding the labels to our previous example:

```yaml
  - trigger: ":tomorrow"
    replace: "{{mytime}}"
    label: "Insert tomorrow's date, such as 5-Jan-2022"
    vars:
      - name: mytime
        type: date
        params:
          format: "%v"
          offset: 86400

  - trigger: ":yesterday"
    replace: "{{mytime}}"
    label: "Insert yesterday's date, such as 5-Jan-2022"
    vars:
      - name: mytime
        type: date
        params:
          format: "%v"
          offset: -86400
```

would be displayed as follows in the Search bar:

![Matches being displayed in the Search Bar with labels](data:image/png;base64,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)

## [Multiple triggers](https://espanso.org/docs/matches/basics/#multiple-triggers)

Sometimes it's useful to expand a snippet using various aliases. Because of this, Espanso supports _multi-trigger_ matches, which allows the user to specify multiple triggers to expand the same match. To use the feature, simply specify a list of triggers in the `triggers` field (instead of `trigger`):

```yaml
  - triggers: ["hello", "hi"]
    replace: "world"
```

Now typing either `hello` or `hi` will be expanded to `world`.

## [Image Matches](https://espanso.org/docs/matches/basics/#image-matches)

Espanso also supports **expanding matches into images**. This can be useful in many situations, such as when writing emails or chatting.

![Image match example](https://espanso.org/assets/images/imagematches-c2246e63acf2020a6ce1674ec6ce05fc.gif)

The syntax is pretty similar to the standard one, except you have to specify `image_path` instead of `replace`. This will be the path to your image.

```yaml
  - trigger: ":cat"
    image_path: "/path/to/image.png"
```

##### Format remarks

On Windows and macOS, the most commonly used formats (such as PNG, JPEG and GIF) should work as expected. On Linux, **you should generally use PNG** as it's the most compatible.

### [Path convention](https://espanso.org/docs/matches/basics/#path-convention)

While you can use any valid path in the `image_path` field, there are times in which it proves limited. For example, if you are synchronizing your configuration across different machines, you could have problems creating the same path on each of them.

In those cases, the best solution is to create a folder into the espanso configuration directory and put all your images there. At this point, you can use the `$CONFIG` variable in `image_path` to avoid hard-coding the path. For example:

Create the `images` folder inside the espanso configuration directory (the one which contains the `match` and `config` directories), and store all your images there. Let's say I stored the `cat.png` image. We can now create a Match with:

```yaml
  - trigger: ":cat"
    image_path: "$CONFIG/images/cat.png"
```

## [Nested Matches](https://espanso.org/docs/matches/basics/#nested-matches)

_Nested matches_ makes it possible to include the output of a match inside another one.

```yaml
  - trigger: ":one"
    replace: "nested"

  - trigger: ":nested"
    replace: "This is a {{output}} match"
    vars:
      - name: output
        type: match
        params:
          trigger: ":one"
```

At this point, if you type `:nested` you'll see `This is a nested match` appear.

## [Forms](https://espanso.org/docs/matches/basics/#forms)

Espanso is capable of creating arbitrarily complex input forms.

![Espanso Form](https://espanso.org/assets/images/macform-e187d4291308dbccb2f2e346be45aa6b.png)

These open up a world of possibilities, allowing the user to create matches with many arguments, as well as injecting those values into custom Scripts or Shell commands.

For more information, visit the [Forms section](https://espanso.org/docs/matches/forms/).

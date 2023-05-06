# May 02, 2023 TIL

## Configure Patched Font with Nerd Font Fallback to Fix Glyph Issues

Set a patched non-NF font with a patched NF font fallback to fix terminal font glyph issues. For example,
set `Fira Code` as the primary font and `MesloLGS Nerd Font Mono` as the fallback font to fix inconsistent sizing or
misaligned glyph issues.

### Wezterm Font with Fallback Configuration

```lua
-- ...

-- cell width per char
config.cell_width = 1.0

-- keeps font glyph sizing consistent by preventing glyphs from overflowing square width
config.allow_square_glyphs_to_overflow_width = "Never"

--- the order of the listed fonts will affect how the font glyphs are displayed
-- 1. set non-NF patched font first
-- 2. set NF patched font second
-- 3. set additional fallback fonts to address any outstanding font issues
config.font = wezterm.font_with_fallback {
  'Fira Code',
  -- 'FiraCode Nerd Font',
  'MesloLGS Nerd Font Mono',
  'codicons-normalized',
  -- macos specific
  'Apple Symbols',
  'Arial Unicode MS',
}

config.font_rules = {
  {
    intensity = 'Bold',
    italic = false,
    font = wezterm.font_with_fallback {
      {
        family = 'Fira Code',
        weight = 'Bold',
      },
      -- {
      --   family = 'FiraCode Nerd Font',
      --   weight = 'Bold',
      -- },
      {
        family = 'MesloLGS Nerd Font Mono',
        weight = 'Bold',
      },
      {
        family = 'codicons-normalized',
        weight = 'Bold',
      },
      {
        family = 'Apple Symbols',
        weight = 'Bold',
      },
      {
        family = 'Arial Unicode MS',
        weight = 'Bold',
      },
    },
  },
  {
    intensity = 'Normal',
    italic = false,
    font = wezterm.font_with_fallback {
      {
        family = 'Fira Code',
        weight = 'Regular',
      },
      -- {
      --   family = 'FiraCode Nerd Font',
      --   weight = 'Regular',
      -- },
      {
        family = 'MesloLGS Nerd Font Mono',
        weight = 'Regular',
      },
      {
        family = 'codicons-normalized',
        weight = 'Regular',
      },
      {
        family = 'Apple Symbols',
        weight = 'Regular',
      },
      {
        family = 'Arial Unicode MS',
        weight = 'Regular',
      },
    },
  },
}

-- ...
```


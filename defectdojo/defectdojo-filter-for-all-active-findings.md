# August 15, 2023 TIL - DefectDojo Filter for All Active Findings

How-to filter for all Active Findings, excluding
Duplicate/Mitigated/Out of Scope/False Positive/Risk Accepted Findings,
for a Product or Products in DefectDojo and
sort the results by Date in descending order (newest findings first).

## How-To Create an All Active Findings Filter

From the DefectDojo Dashboard:

1. Navigate to the All Findings page

![How-To Create an All Active Findings Filter - Step 1](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings1.png)

2. Click the Filters dropdown menu

![How-To Create an All Active Findings Filter - Step 2](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings2.png)

3. Set your Product Filter

![How-To Create an All Active Findings Filter - Step 3](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings3.png)

4. Set your Active Filter
    - Unknown: Includes both Active/Inactive Findings
    - Yes: Includes Active; Excludes Inactive Findings
    - No: Excludes Active; Includes Inactive Findings

![How-To Create an All Active Findings Filter - Step 4](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings4.png)

5. Set your Duplicate Filter
    - Either: Includes Both Original/Duplicate Findings
    - Yes: Excludes Original; Includes Duplicate Findings
    - No: Includes Original; Excludes Duplicate Findings

![How-To Create an All Active Findings Filter - Step 5](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings5.png)

6. Set your Mitigated Filter
    - Either: Includes Both Mitigated/Non-Mitigated Findings
    - Yes: Includes Mitigated; Excludes Non-Mitigated Findings
    - No: Excludes Mitigated; Includes Non-Mitigated Findings

![How-To Create an All Active Findings Filter - Step 6](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings6.png)

7. Set your Out Of Scope Filter
    - Unknown: Includes Both In Scope/Out Of Scope Findings
    - Yes: Excludes In Scope; Includes Out Of Scope Findings
    - No: Includes In Scope; Excludes Out Of Scope Findings

![How-To Create an All Active Findings Filter - Step 7](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings7.png)

8. Set your False Positive Filter
    - Unknown: Includes Both Non-False Positive/False Positive Findings
    - Yes: Excludes Non-False Positive; Includes False Positive Findings
    - No: Includes Non-False Positive; Excludes False Positive Findings

![How-To Create an All Active Findings Filter - Step 8](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings8.png)

9. Set your Risk Accepted Filter
    - Unknown: Includes Both Non-Risk Accepted/Risk Accepted Findings
    - Yes: Excludes Non-Risk Accepted; Includes Risk Accepted Findings
    - No: Includes Non-Risk Accepted; Excludes Risk Accepted Findings

![How-To Create an All Active Findings Filter - Step 9](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings9.png)

10. Set your Ordering (Sort) Filter

![How-To Create an All Active Findings Filter - Step 10](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings10.png)

11. Click Apply Filters

![How-To Create an All Active Findings Filter - Step 11](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings11.png)

12. Notice the difference in total findings before/after applying the filters

![How-To Create an All Active Findings Filter - Step 12](https://raw.githubusercontent.com/cleong14/til/main/assets/defectdojo/defectdojo-filter-for-all-active-findings12.png)

<details>
    <summary><strong><i>Do you find yourself setting the same filters over and over again?</i></strong></summary>

    Pro Tip:

    After clicking Apply Filters, you can save your filters by saving the page
    as a bookmark in your web browser.

    Now you can quickly access and reuse filters by navigating to the saved
    bookmarks.
</details>

## Use Cases

- Filter for all Active Findings in DefectDojo
- How-to create and save a new filter in DefectDojo

## References

- [All Active Findings - Demo Site | DefectDojo](https://demo.defectdojo.org/finding?test_import_finding_action__test_import=&title=&component_name=&component_version=&date=&last_reviewed=&last_status_update=&mitigated=&test__engagement__product=4&test__engagement__version=&test__version=&status=&active=true&verified=unknown&duplicate=2&is_mitigated=2&out_of_scope=false&false_p=false&risk_accepted=false&has_component=unknown&has_notes=unknown&file_path=&unique_id_from_tool=&vuln_id_from_tool=&service=&param=&payload=&risk_acceptance=&has_finding_group=unknown&tags=&test__tags=&test__engagement__tags=&test__engagement__product__tags=&tag=&not_tags=&not_test__tags=&not_test__engagement__tags=&not_test__engagement__product__tags=&not_tag=&vulnerability_id=&planned_remediation_date=&planned_remediation_version=&endpoints__host=&o=-date)


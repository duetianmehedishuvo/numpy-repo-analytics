# PhD Candidate Coding Exercise - Repository Insight Analysis


The goal of this analysis was to extract commit-level data from the `numpy/numpy` GitHub repository, analyze the frequency of changes, and visualize trends in code churn (insertions and deletions) for specific files and file types over time. This exercise also includes critical reflection on the findings and any challenges encountered during the process.

---

## Research Question

For this analysis, **RQ2: "Which files are changed most frequently, and what file types dominate the churn?"** was selected. This research question focuses on identifying the most frequently modified files and understanding the types of files (by extension) that experience the highest code churn (lines added and removed).

---

## Data Collection

### Methodology

* **Repository**: The data was extracted from the `numpy/numpy` GitHub repository using the **PyDriller** library, which enables easy mining of commit history and metadata.
* **Commit Information Collected**:

  * **Author**: The name of the author who made the changes.
  * **Timestamp**: The commit timestamp (converted to Unix timestamp for consistency).
  * **Files**: The files modified, including their path, insertions, deletions, and file extension.

The script traverses all commits in the repository and aggregates the changes to track the most frequently modified files, the total code churn per file type, and the authors contributing to each file.

---

## Code

The analysis was performed using Python, leveraging the following libraries:

* **PyDriller**: To mine the commit history of the repository.
* **Pandas**: For data manipulation and organization.
* **Matplotlib** and **Seaborn**: For data visualization.

### Key Sections of the Code:

1. **Data Collection**:

   * Extracted relevant commit data such as the number of insertions, deletions, and modified files.
   * Aggregated the data into a dictionary, and converted it into a pandas DataFrame.
2. **Visualization**:

   * **Top 10 Most Frequently Changed Files**: A bar chart was created to visualize which files had the most changes.
   * **Code Churn by File Type**: Another bar chart was created to show which file types (extensions) had the most code churn (insertions + deletions).

Both visualizations are saved as images for easy reference.

---

## Issues Encountered

### Git Version Compatibility Issue

While using **PyDriller** (version 2.7) to extract data from the `numpy/numpy` repository, I encountered the following error due to a **Git version mismatch**:

* **Error Message**:
  `"GitVersion: Current git version is 2.34. Minimum supported version is 2.38."`

This error arose because **PyDriller 2.7** required **Git 2.38** or later, while I was using **Git 2.34**. I attempted to update my Git version to the latest one, but the issue persisted. After several unsuccessful attempts, I found that upgrading Git did not resolve the problem.

### Solution Implemented

After further investigation and research through Google, I discovered that **PyDriller version 1.15** did not have this version dependency on Git and worked well with older Git versions (like 2.34).

* **Solution**: I downgraded **PyDriller** to version 1.15, and it resolved the compatibility issue, allowing the analysis to run smoothly.

### Tools Used:

* **Google Search**: I used Google search to troubleshoot and resolve the issue. The solution was to downgrade to **PyDriller 1.15** instead of upgrading the Git version.

This issue was resolved without relying on AI tools like ChatGPT.

---

## Visualizations

1. **Top 10 Most Frequently Changed Files**:

   * This visualization shows the files with the highest number of changes across all commits in the repository.

   ![top_changed_files](https://github.com/user-attachments/assets/0f8a7fd6-f5e4-49eb-9317-6437fe873e05)


3. **Top File Types by Code Churn**:

   * This visualization displays the most churned file types (extensions), summing both insertions and deletions to represent the total code churn for each file type.

   ![file_type_churn](https://github.com/user-attachments/assets/f4961c56-12d3-48f7-854f-1e207c481938)


---

## Reflection

### Challenges and Errors Encountered:

* **Data Quality**: One of the challenges faced was missing data for some commits, particularly for files where the commit might not have involved any file changes (e.g., documentation or metadata changes). This was handled by filtering out such commits early on.

* **Handling Date and Time**: There were occasional issues with handling commit timestamps across different time zones. However, using `committer_date` provided a consistent method for handling commit times across all commits.

* **PyDriller Limitations**: While PyDriller worked well for this project, its processing speed could be slow for larger repositories with extensive histories. This could be addressed by limiting the number of commits analyzed or optimizing data collection methods.

### Surprising or Ambiguous Findings:

* **File Extensions and Churn**: It was surprising to see that certain file types (e.g., `.py` and `.c`) experienced a disproportionately high amount of churn, even though they were not necessarily the most frequently modified. This might indicate that these files have higher levels of active development or are more prone to refactoring.

* **Ambiguous Trends**: The trends in churn for different file types might be influenced by external factors, such as larger refactoring efforts or the introduction of major features. Further investigation into commit messages could provide clarity.

### Follow-Up Questions:

* **Impact of Refactoring**: How does refactoring (e.g., code cleanup, renaming) influence the overall churn of a file type? It would be interesting to track and analyze commits specifically focused on refactoring changes.

* **Author Impact**: What role do different contributors play in modifying particular file types? A deeper dive into author-specific trends could yield valuable insights on development practices and collaboration.

---

## Conclusion

This exercise provided valuable insights into how files in the `numpy/numpy` repository have evolved. By analyzing the frequency of changes and the associated code churn, we can better understand development trends and the role of different file types in the project’s history. Further analysis can build on this foundation to explore deeper relationships between code changes, authors, and file types.

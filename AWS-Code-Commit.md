### AWS CodeCommit

Provides the ability to host highly **scalable private Git repositories** and collaborate on code.
* Removes the need to host, maintain, back up, or scale source control servers
* Customize user-specific access to repositories with automatically encrypted files in transit
* Keep repositories highly available and accessible with scalable, redundant, and durable architecture
* Maintain your repositories close to build, staging, and production environments on AWS

![image](https://user-images.githubusercontent.com/114364831/211430777-b10f4cc8-a8de-4f7d-bde5-41b20254ef89.png)

Cases in which CodeCommit is not the correct solution:

**Use case:**

* Large files that change frequently

**Description:**

* Git uses **delta encoding** to store differences between versions of files. For example, if you change a few words in a document, Git will only store those changed words. If you have files or objects over 5 MB with many changes, Git might need to reconstruct a large chain of delta differences. This can consume an increasing amount of compute resources on both your local computer and in CodeCommit as these files grow over time.

**Solution:**

* To version large files, consider Amazon Simple Storage Service (Amazon S3)


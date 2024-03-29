# 2024-01-14 TIL - Log GitLab CI Output to Stderr

To read the standard error output (stderr) logs used in GitLab CI, you can use the `gitlab-ci.yml` configuration file to define your job and specify the script or command to run. When a command or script produces an error, it will be captured in the stderr logs.


## Usage

Here's an example of how you can read the stderr logs in GitLab CI:

```yaml
stages:
  - build

job1:
  stage: build
  script:
    - echo "This is a sample error message" >&2
  allow_failure: true
```

In the above example:

1. The `job1` stage is defined with a script that echoes a sample error message to stderr using `>&2`
2. The `allow_failure` flag is set to `true` to allow the job to complete even if it fails

After running the GitLab CI pipeline, you can view the stderr logs for the job by navigating to the job details page. Look for the "Job log" section, where you'll find the complete logs, including any error messages generated by the script.


## Use Cases

- Output GitLab CI logs to stderr but not stdout
- Debug GitLab CI jobs without logging to stdout


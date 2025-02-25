# Gitlab Sonar Scanner & Quality Gate

Work inspired by [ciricihq/gitlab-sonar-scanner](https://github.com/ciricihq/gitlab-sonar-scanner)

Using it in your gitlab projects
--------------------------------

Add the next stage to your `.gitlab-ci.yml`.

~~~yaml
stages:
- quality-gate

sonarqube:
  stage: quality-gate
  image: 01123581321345589144233377/gitlab-sonar-scanner:1.1.2
  variables:
      SONAR_URL: https://your.sonarqube.server
      SONAR_LOGIN: "${SONAR_TOKEN}"
      SONAR_PROJECT_KEY: "${CI_PROJECT_NAME}"
      SONAR_PROJECT_NAME: "${CI_PROJECT_TITLE}"
  script:
    - gitlab-sonar-scanner
    - sonar_qg
~~~

If you need to add a specific configuration, you can also create a `sonar-project.properties` file.


Samples of output in Gitlab-CI
--------------------------------

![Output](docs/cli_result.png?raw=true "CLI Output")


Appending Sonar Quality Gate's result into your Merge Request
--------------------------------------------------------------

Prerequisite:
* Generate a [Gitlab personal access token](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html) with the scope *api*
* Add the next stage to your `.gitlab-ci.yml`
* Open a merge request

~~~yaml
stages:
- quality-gate

sonarqube:
  stage: quality-gate
  image: 01123581321345589144233377/gitlab-sonar-scanner:1.1.2
  variables:
      SONAR_URL: https://your.sonarqube.server
      SONAR_LOGIN: "${SONAR_TOKEN}"
      SONAR_PROJECT_KEY: "${CI_PROJECT_NAME}"
      SONAR_PROJECT_NAME: "${CI_PROJECT_TITLE}"
  script:
    - gitlab-sonar-scanner
    - sonar_qg --gitlab_personal_token "${GITLAB_PERSONAL_TOKEN}"
~~~

Output in Gitlab Merge Request
--------------------------------

![Merge Request Output](docs/merge_request_result.png?raw=true "Merge Request  Output")

sonar_qg parameters
--------------------------------

```
Sonar Quality Gate CLI 1.0.0

USAGE:
    sonar_qg [FLAGS] [OPTIONS] [report-task-path]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information
    -v, --verbose    Verbose mode (-v, -vv, -vvv, etc.)

OPTIONS:
    -g, --gitlab_personal_token <gitlab-personal-token>     [env: GITLAB_PERSONAL_TOKEN=]

ARGS:
    <report-task-path>     [default: .scannerwork/report-task.txt]
```

License
=======

All the code contained in this repository is licensed under a MIT License.

See [LICENSE](LICENSE) for more details

Contribution
============

All contribution are more than welcomed!
If you need more information about contribution, details are in [CONTRIBUTING.md](CONTRIBUTING.md)

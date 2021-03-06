# merge-schedule-action

> GitHub Action to merge pull requests on a scheduled day

## Usage

Create `.github/workflows/merge-schedule.yml`

```yml
name: Merge Schedule
on:
  pull_request:
    types:
      - opened
      - edited
  schedule:
    # https://crontab.guru/every-hour
    - cron: 0 * * * *

jobs:
  merge_schedule:
    runs-on: ubuntu-latest
    steps:
      - uses: gr2m/merge-schedule-action@v1.x
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

In your pull requests, add a line to the end of the pull request description look looking like this

```
/schedule 2019-12-31
```

To control at which time of the day you want the pull request to be merged, I recommend to adapt the `- cron: ...` setting in the workflow file.

The action sets a pending commit status if the pull request was recognized as being scheduled.

Note that pull requests from forks are ignored for security reasons.

## License

[ISC](LICENSE)

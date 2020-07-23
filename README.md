This repo includes an example of an Azure deployment GitHub workflow that has
been instrumented with user-defined CTO.ai Delivery Metrics. This
instrumentation is achieved using the [CTO.ai GitHub Action](https://github.com/cto-ai/action).

The key portion of the example Workflow is here:

```
- name: Report Build Succeeded
  if: ${{ success() }}
  uses: ctoai/action@v1-beta
  id: ctoai-build-succeeded
  with:
    team_id: ${{ secrets.CTOAI_TEAM_ID }}
    token: ${{ secrets.CTOAI_EVENTS_API_TOKEN }}
    stage: "Build"
    status: "Succeeded"
    change-id: "your-change-id1"
    pipeline-id: "your-pipeline-id1"
- name: Report Build Failed
  if: ${{ failure() }}
  uses: ctoai/action@v1-beta
  id: ctoai-build-failed
  with:
    team_id: ${{ secrets.CTOAI_TEAM_ID }}
    token: ${{ secrets.CTOAI_EVENTS_API_TOKEN }}
    stage: "Build"
    status: "Failed"
    change-id: "your-change-id1"
    pipeline-id: "your-pipeline-id1"
```

Notice how `cto-ai/action` is invoked once to send an event to the CTO.ai
Delivery Metrics dashboard.

The CTO.ai GitHub Action accepts the same parameters as the regular CTO.ai
Delivery Metrics APIs, which are explained in greater detail at the
[CTO.ai Official Documentation](cto.ai/docs/delivery-metrics).


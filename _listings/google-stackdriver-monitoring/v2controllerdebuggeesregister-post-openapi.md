---
swagger: "2.0"
x-collection-name: Google Stackdriver Monitoring
x-complete: 0
info:
  title: Google Stackdriver Monitoring Post Controller Debuggees Register
  description: Registers the debuggee with the controller service. All agents attached
    to the same application should call this method with the same request content
    to get back the same stable `debuggee_id`. Agents should call this method again
    whenever `google.rpc.Code.NOT_FOUND` is returned from any controller method. This
    allows the controller service to disable the agent or recover from any data loss.
    If the debuggee is disabled by the server, the response will have `is_disabled`
    set to `true`.
  version: 1.0.0
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /v2/controller/debuggees/register:
    post:
      summary: Post Controller Debuggees Register
      description: Registers the debuggee with the controller service. All agents
        attached to the same application should call this method with the same request
        content to get back the same stable `debuggee_id`. Agents should call this
        method again whenever `google.rpc.Code.NOT_FOUND` is returned from any controller
        method. This allows the controller service to disable the agent or recover
        from any data loss. If the debuggee is disabled by the server, the response
        will have `is_disabled` set to `true`.
      operationId: clouddebugger.controller.debuggees.register
      x-api-path-slug: v2controllerdebuggeesregister-post
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      responses:
        200:
          description: OK
      tags:
      - Debugger
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---
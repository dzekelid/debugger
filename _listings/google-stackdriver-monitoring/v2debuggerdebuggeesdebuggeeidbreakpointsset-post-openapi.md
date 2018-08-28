---
swagger: "2.0"
x-collection-name: Google Stackdriver Monitoring
x-complete: 0
info:
  title: Google Stackdriver Monitoring Post Debugger Debuggees Debuggeeid Breakpoints
    Set
  description: Sets the breakpoint to the debuggee.
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
  /v2/controller/debuggees/{debuggeeId}/breakpoints:
    get:
      summary: Get Controller Debuggees Debuggeeid Breakpoints
      description: Returns the list of all active breakpoints for the debuggee. The
        breakpoint specification (location, condition, and expression fields) is semantically
        immutable, although the field values may change. For example, an agent may
        update the location line number to reflect the actual line where the breakpoint
        was set, but this doesn't change the breakpoint semantics. This means that
        an agent does not need to check if a breakpoint has changed when it encounters
        the same breakpoint on a successive call. Moreover, an agent should remember
        the breakpoints that are completed until the controller removes them from
        the active list to avoid setting those breakpoints again.
      operationId: clouddebugger.controller.debuggees.breakpoints.list
      x-api-path-slug: v2controllerdebuggeesdebuggeeidbreakpoints-get
      parameters:
      - in: path
        name: debuggeeId
        description: Identifies the debuggee
      - in: query
        name: successOnTimeout
        description: If set to `true`, returns `google
      - in: query
        name: waitToken
        description: A wait token that, if specified, blocks the method call until
          the list of active breakpoints has changed, or a server selected timeout
          has expired
      responses:
        200:
          description: OK
      tags:
      - Debugger
  /v2/controller/debuggees/{debuggeeId}/breakpoints/{id}:
    put:
      summary: Put Controller Debuggees Debuggeeid Breakpoints
      description: Updates the breakpoint state or mutable fields. The entire Breakpoint
        message must be sent back to the controller service. Updates to active breakpoint
        fields are only allowed if the new value does not change the breakpoint specification.
        Updates to the `location`, `condition` and `expression` fields should not
        alter the breakpoint semantics. These may only make changes such as canonicalizing
        a value or snapping the location to the correct line of code.
      operationId: clouddebugger.controller.debuggees.breakpoints.update
      x-api-path-slug: v2controllerdebuggeesdebuggeeidbreakpointsid-put
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: path
        name: debuggeeId
        description: Identifies the debuggee being debugged
      - in: path
        name: id
        description: Breakpoint identifier, unique in the scope of the debuggee
      responses:
        200:
          description: OK
      tags:
      - Debugger
  /v2/debugger/debuggees:
    get:
      summary: Get Debugger Debuggees
      description: Lists all the debuggees that the user can set breakpoints to.
      operationId: clouddebugger.debugger.debuggees.list
      x-api-path-slug: v2debuggerdebuggees-get
      parameters:
      - in: query
        name: clientVersion
        description: The client version making the call
      - in: query
        name: includeInactive
        description: When set to `true`, the result includes all debuggees
      - in: query
        name: project
        description: Project number of a Google Cloud project whose debuggees to list
      responses:
        200:
          description: OK
      tags:
      - Debugger
  /v2/debugger/debuggees/{debuggeeId}/breakpoints:
    get:
      summary: Get Debugger Debuggees Debuggeeid Breakpoints
      description: Lists all breakpoints for the debuggee.
      operationId: clouddebugger.debugger.debuggees.breakpoints.list
      x-api-path-slug: v2debuggerdebuggeesdebuggeeidbreakpoints-get
      parameters:
      - in: query
        name: action.value
        description: Only breakpoints with the specified action will pass the filter
      - in: query
        name: clientVersion
        description: The client version making the call
      - in: path
        name: debuggeeId
        description: ID of the debuggee whose breakpoints to list
      - in: query
        name: includeAllUsers
        description: When set to `true`, the response includes the list of breakpoints
          set by any user
      - in: query
        name: includeInactive
        description: When set to `true`, the response includes active and inactive
          breakpoints
      - in: query
        name: stripResults
        description: 'When set to `true`, the response breakpoints are stripped of
          the results fields: `stack_frames`, `evaluated_expressions` and `variable_table`'
      - in: query
        name: waitToken
        description: A wait token that, if specified, blocks the call until the breakpoints
          list has changed, or a server selected timeout has expired
      responses:
        200:
          description: OK
      tags:
      - Debugger
  /v2/debugger/debuggees/{debuggeeId}/breakpoints/set:
    post:
      summary: Post Debugger Debuggees Debuggeeid Breakpoints Set
      description: Sets the breakpoint to the debuggee.
      operationId: clouddebugger.debugger.debuggees.breakpoints.set
      x-api-path-slug: v2debuggerdebuggeesdebuggeeidbreakpointsset-post
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: query
        name: clientVersion
        description: The client version making the call
      - in: path
        name: debuggeeId
        description: ID of the debuggee where the breakpoint is to be set
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
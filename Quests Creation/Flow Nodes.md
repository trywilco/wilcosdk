# Flow Nodes

When the step starts or when the user performs an action (trigger) that the step expects, a logical flow will be executed. The flow is defined using flow nodes.  Each flow node consists of `do`, `if`, and `switch` blocks. 

![Untitled](Flow%20Nodes/FlowNode.jpeg)

Each flow node contains any of the following:

- **do:** list of actions to perform.
    
    ```yaml
    do:
    - actionId: <action_1>
      params:
        ...
    - actionId: <action_2>
      params:
        ...
      paramsFramework:
        node:
            ...
        python:
          ...
        rails:
          ...
    ```
    
- **if**: conditional statement. **if** statements evaluate conditions and continue to **then** or **else** flow node according to the result. The result is considered successful if all conditions are met  ( `condition_1 && condition_2 && condition_3` )
    
    ```yaml
    if:
      conditions:
      - conditionId: <condition 1>
        params:
          ...
      - conditionId: <condition 2>
        params:
          ...
    
      then:
        do:
          ...
        if:
         ...
    
      else:
        do:
          ...
        if:
          ...
    ```
    
- **switch**: switch statement. **switch** evaluates a **key** property and continues to the appropriate flow node (one of the **cases**) according to the result.
    
    ```yaml
    switch:
      key: <key>
        cases:
          case_1:
            do:
              ...
            if:
              ...
        case_2:
          do:
            ...
          if:
            ...
    ```

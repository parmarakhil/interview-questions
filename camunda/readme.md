Camunda BPM

1. BPM
    1.  BPM stands for Business Process Management. It is a set of activities which follows the number of steps in a specific order to fulfill the organizational goals. The order of these goals is depicted using a flowchart.
    2. It involves:
        1. Understanding the values which the organization delivers.
        2. How those are achieved by analyzing, documenting and improving the way that people and systems work together.
2. Variables vs input parameters
    1. input/output can be used on any activity in order to map a global variable to a local variable.
    2. The Variables tab is there for sending variables from the parent process to the called child process.
3. BPMN
    1. The Business Process Modeling Notation (BPMN) is visual modeling language for business analysis applications and specifying enterprise process workflows, which is an open standard notation for graphical flowcharts that is used to define business process workflows. 
    2. It is popular and intuitive graphic that can be easily understand by all business stakeholders, including business users, business analysts, software developers, and data architects.
    3. Benefits
        1. An industry standard developed by the OMG consortium, a not-for-profit industry group
        2.  Provides businesses with the capability of defining and understanding their procedures through Business Process Diagrams
        3.  To provide a standard notation that is readily understandable by all business stakeholders
        4.  To bridge the communication gap that frequently occurs between business process design and implementation
        5.  Simple to learn yet powerful enough to depict the potential complexities of a business process
4. Camunda modeler
    1. Camunda Modeler is a user-friendly desktop application that gives developers powerful features for designing and deploying automated processes, human workflows, decision tables, and decision requirements diagrams using the globally recognized BPMN and DMN standards.
5. Camunda cockpit 
    1. Cockpit gives you a real-time view of BPMN processes and DMN decision tables as they run, so you can monitor their status and quickly identify technical incidents that slow down or stop workflows.
6. Gateways
    1. Exclusive gateway
        1. An exclusive gateway evaluates the state of the business process and based on the condition, breaks the flow into one of the two or more mutually exclusive paths
    2. Event based gateway
        1. It is similar to exclusive gateway because both involve one path in the flow. In the case of event based gateway, you evaluate which event has occurred not which condition has been met
    3. Paralle gateway
        1. In this gateway you don’t evaluate any condition or event. Instead, a parallel gateway is used to represent two concurrent tasks in a business flow
    4. Parallel event based gateway
        1. Similar to parallel gateway. It allows for multiple processes to happen at the same time, but unlike the parallel gateway, the processes depend on specific events
    5. Inclusive gateway
        1. An inclusive gateway breaks the process flow into one or more flows. 

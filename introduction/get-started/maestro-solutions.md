---
description: >-
  Explore Maestro's ecosystem: Studio, CLI, Cloud, Flows, and JavaScript
  integration.
---

# Maestro solutions

The Maestro ecosystem is a unified platform composed of three interconnected layers. Each tool is designed to solve a specific challenge in the mobile and web automation lifecycle:&#x20;

* **Maestro Studio**: Desktop IDE for writing and running Maestro flows
* **Maestro CLI**: Command line tool for running Maestro flows
* **Maestro Cloud**: Hosted platform for consistent, parallel Maestro execution

### **Maestro Studio (The IDE)**

Maestro Studio is a visual interface built on top of the CLI, designed for rapid test creation and real-time element inspection. By mirroring your device screen and allowing you to build [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) through simple point-and-click interactions, it serves as the primary tool for zero-code authoring and interactive debugging.&#x20;

You can start building your first Flows today by visiting the [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/) documentation.

### **Maestro CLI**&#x20;

The CLI is the open-source heart of Maestro and the core engine that powers both Maestro Studio and Maestro Cloud. It serves as the workhorse for developers and DevOps engineers, interpreting your YAML files to orchestrate test execution. Because everything else is built on top of the CLI, it acts as the foundational backbone for all local automation and CI/CD integration.

To learn more about its technical capabilities and orchestration features, check out the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/) documentation.

### **Maestro Cloud**

Maestro Cloud is a managed execution solution designed to scale your testing infrastructure without the overhead of managing local device farms. It leverages the Maestro CLI to run your tests on a distributed cloud of virtual devices, enabling massive parallelization and providing fast and reliable feedback loops for production-ready reliability.

Explore how to scale your regression suites in the [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/) documentation.&#x20;

### Which solution should I use?

Use the table below to determine which tool fits your current workflow:

| **Feature**     | **Maestro Studio**      | **Maestro CLI**         | **Maestro Cloud**           |
| --------------- | ----------------------- | ----------------------- | --------------------------- |
| **Best For**    | Authoring & Debugging   | Automation & CI/CD      | Mass Regression & Speed     |
| **Interface**   | Visual (GUI)            | Terminal (Command Line) | Managed Infrastructure      |
| **Execution**   | Real-time / Interactive | Sequential (Local)      | Parallel (Simultaneous)     |
| **Target User** | QA & Developers         | Engineers & DevOps      | Growth & Professional Teams |
| **Environment** | Local Device/Emulator   | Local Device/Emulator   | Hosted Virtual Devices      |

### The typical learning path

Most teams follow a three-stage journey to automation success:

1. **Creation**: Start with [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/) to visually build and debug your first [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/).
2. **Automation**: Use the[ Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/) to run those Flows locally and integrate them into your basic development workflow.
3. **Scaling**: Once your test suite grows, transition to [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/) to run those same tests in parallel for instant feedback on every Pull Request.

### Next steps

If you already know the Maestro solution you are going to use, access the desired documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)

If you don't know how to create tests with Maestro, access the [QuickStart](quickstart.md) guide to get up and running in minutes.

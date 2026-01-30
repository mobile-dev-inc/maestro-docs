# Designe your test architecture

Moving from your first test to a full-scale automation suite requires shifting your focus from "how to write a command" to "how to design a system." A well-architected Maestro suite ensures that your tests stay fast, reliable, and easy to maintain as your application evolves.

To build this system, you need to address two distinct layers:&#x20;

* Where your tests live&#x20;
* How they are structured

To help you navigate these layers, you can explore the best practices into the following specialized guides:

1. [Repository configuration](repository-configuration.md): Learn where to store test files or choosing a high-level organization model (User Journeys vs. Features). It will help you decide on your folder structure and repo strategy, preventing refactoring later.
2. [Structuring your test suite](https://maestro.dev/blog/maestro-best-practices-structuring-your-test-suite): Check this guide if you are ready to write YAML files and want to know the rules for naming, sub-folders, and using tags to filter execution. Learn the "Maestro Way" of writing modular, tagged, and parallel-ready tests.

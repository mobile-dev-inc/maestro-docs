# Web desktop support in Maestro

While Maestro is primarily known as a "mobile-first" testing framework, its long-term vision is to become "one framework to rule them all." This includes support for **automated testing of web applications in desktop browsers**, enabling unified test automation across platform boundaries.

{% hint style="warning" %}
Web support is currently in **Work in Progress** status. It's functional but at an earlier maturity stage compared to Android and iOS support.
{% endhint %}

## Architecture and philosophy

Maestro maintains its "Arm's Length" philosophy for web testing:
- **Platform-Agnostic Interaction:** Tests simulate user interactions rather than directly manipulating DOM elements or injecting JavaScript
- **Unified YAML Syntax:** The same `.yaml` specification used for mobile tests applies to web, reducing context switching and tooling complexity
- **User-Centric Validation:** Focus on end-to-end user flows over implementation details

## Use cases

To help you understand the scenarios you can test with Maestro with a web browser, here is a short list of use cases.

### Ideal scenarios
- **Hybrid Projects for Mobile and Web:** Teams already using Maestro for mobile can extend coverage to web without learning new frameworks
- **React Native Web:** Projects using shared codebases across mobile and web platforms
- **Cross-Platform Test Suites:** Applications requiring consistent test coverage across multiple deployment targets

### Alternative considerations
For **pure web applications**, dedicated tools like Playwright or Cypress may offer more granular control and extensive web-specific features.

### Test execution
- Tests execute against live browser instances via WebDriver protocols
- Command syntax remains consistent: `tapOn`, `inputText`, visual assertions work across platforms
- No DOM manipulation or JavaScript injection required

### Current limitations
- Feature set optimized for primary use cases
- Documentation reflects mobile-first historical focus with over 90% of the user base
- Some advanced web-specific features not yet implemented

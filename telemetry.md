## Telemetry

Mark Sharp collects basic telemetry for the purpose of identifying and diagnosing bugs to improve the product.  **Mark Sharp does not collect any personally identifiable information such as user credentials, Markdown contents, or file names.** Mark Sharp follows the telemetry policy of VS Code - if you opt out of reporting telemetry for VS Code itself, then telemetry for Mark Sharp will also not be collected.

The following table outlines the types of data points collected:

| Event Name         | Description                                                                       | Fields       |
| ------------------ | --------------------------------------------------------------------------------- | ------------ |
| activated          | The Mark Sharp extension was activated                                            | _none_       |
| activation-error   | An error occurred during license activation                                       | licenseKey   |
| deactivation-error | An error occurred during license activation                                       | licenseKey   |
| webview-error      | The Mark Sharp webview threw an error (either from markdown parsing or rendering) | errorMessage |
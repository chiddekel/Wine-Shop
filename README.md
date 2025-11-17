# Wine-Shop
The wine shop - uwp/APPX/winrt


# Wine Runtime Extension — AppX / WinRT / Offline Runtime Support

This repository tracks technical work required to extend Wine with the ability to
install and operate **offline-distributed modern Windows runtimes**, including:

- AppX / MSIX packaged components  
- WinRT (Windows Runtime) activation  
- Minimal AppModel / AppContainer compatibility  
- Offline installer workflows (PowerShell-based or bundled)  

The objective is to enable Wine to accept, deploy and activate modern Windows
runtime packages **without relying on Microsoft Store or Windows Update**.

---

## 📦 AppX / MSIX Runtime Tasks

- **Implement `appx.dll` base skeleton**  
  Provide module structure and initial stubs.

- **AppX manifest parser**  
  Parse `AppxManifest.xml` (identity, version, dependencies, capabilities).

- **AppX blockmap support**  
  Parse and validate `AppxBlockMap.xml` (file hashes).

- **Define package installation layout**  
  Map `%LOCALAPPDATA%/Packages/<PackageFamily>` within Wine prefix.

- **Implement file extraction handler**  
  Extract package payload files according to manifest.

- **Add `Add-AppxPackage` shim**  
  Implement Wine-native handling of offline AppX/MSIX installation.

- **Registry writer for AppX packages**  
  Add minimal registry entries required by packaged components.

- **Add debug channel `+appx`**  
  Trace manifest, blockmap and installation steps.

---

## ⚙️ WinRT Activation Tasks

- **Implement `RoGetActivationFactory`**  
  Provide runtimeclass lookup and factory routing.

- **Implement `RoActivateInstance`**  
  Return stub WinRT objects matching ABI expectations.

- **WinMD metadata loader**  
  Load `.winmd` metadata and expose runtimeclasses.

- **Runtimeclass registry**  
  Map runtimeclass names to Wine handlers or stubs.

- **Minimal `IInspectable` ABI**  
  Provide base interface and binary layout.

- **Add debug channel `+winrt`**  
  Trace activation requests and failures.

---

## 🛡️ AppContainer Compatibility Tasks

- **Synthetic AppContainer token**  
  Generate fake SIDs, integrity levels, token flags.

- **Capability fallback behavior**  
  Gracefully accept unknown capabilities.

- **AppContainer directory mapping**  
  Provide LocalState, TempState and related paths in prefix.

- **Simulate AppContainer environment variables**  
  Add expected AppModel environment keys.

- **Add debug channel `+appmodel`**  
  Trace AppContainer-related operations.

---

## 📤 Offline Deployment Tasks

- **Offline deployment orchestrator**  
  Coordinate manifest parsing, extraction and registry setup.

- **PowerShell `Add-AppxPackage` redirection**  
  Redirect PowerShell-based installation to Wine handlers.

- **Installer filesystem consistency checker**  
  Validate extracted structure and manifest expectations.

- **Registry provisioning for offline deployments**  
  Create minimal AppModel registry keys.

- **Add debug channel `+deploy`**  
  Log deployment operations in detail.

---

## 🧰 Developer Tooling Tasks

- **CLI tool: `wine-appx-list`**  
  List installed AppX/MSIX packages inside prefix.

- **CLI tool: `wine-winrt-scan`**  
  Enumerate runtimeclasses and available WinMD metadata.

- **Deployment log formatter**  
  Produce readable error messages for failure cases.

- **Activation error classifier**  
  Categorize runtimeclass resolution errors.

- **Documentation: “Debugging packaged Windows runtimes under Wine”**

---

## 🛒 WineShop Runtime Tasks (Concept)

- **Runtime installation format**  
  Define how offline Windows runtimes are described and installed.

- **Runtime manifest specification**  
  JSON/YAML format for describing component sets.

- **Runtime store implementation**  
  Prefix-local storage for installed runtimes.

- **CLI: `wineshop install-runtime`**  
  Install a user-provided runtime package.

- **CLI: `wineshop verify-runtime`**  
  Validate integrity and manifest structure.

- **Documentation: “WineShop Runtime Architecture”**

---

## ✔️ Status
Specification and task definition. Implementation pending.

## 🤝 Contributing
Contributions, prototypes and design discussions are welcome.  
This repository serves as an open workspace for expanding Wine's modern-runtime compatibility.

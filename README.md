UBE-GUI: Web UI to extract Unity asset bundles from games

https://github.com/miki1044/UBE-GUI/releases

![UBE-GUI banner](https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?auto=format&fit=crop&w=1200&q=60)

Table of contents
- Overview
- Core concepts
- Features
- How it works
- Getting started
- Installation
- Quick start guide
- Uploading, analyzing, selecting, and exporting assets
- Advanced usage
- Docker and deployment
- Security, privacy, and best practices
- Architecture and design decisions
- Testing and quality
- Extending and contributing
- Roadmap and future work
- Troubleshooting
- Release assets and downloads
- FAQ
- License
- Credits and acknowledgments
- Topics

Overview
UBE-GUI is a user-friendly web interface designed to help you extract Unity asset bundles from game files. The goal is to provide a smooth, visual workflow: upload a game file, inspect its Unity assets, select the assets you need, and download them as a ZIP archive. The project is built with Python, Flask, and UnityPy, a popular library for Unity asset extraction. The web interface makes asset extraction approachable for modding communities, researchers, and developers who want to study Unity content without diving into low-level code.

This project targets developers and hobbyists who want a streamlined way to explore Unity game content. It focuses on safety, simplicity, and transparency. You can run it locally on your machine or deploy it in a containerized environment to share a consistent setup with teammates. The design emphasizes modularity, so you can customize asset layouts, extraction rules, and export formats to fit your workflow.

Core concepts
- Unity asset bundles: Unity packs data into bundles that can contain textures, meshes, audio, prefabs, and other resources. You can inspect them with UnityPy and related tools.
- Asset selection: After analysis, you choose specific assets to export. This keeps export results focused and reduces noise.
- ZIP export: The final output is a ZIP archive containing the selected assets, organized in a logical structure for easy use in mods, studies, or project pipelines.
- Web-based workflow: A browser-based UI eliminates the need for heavy client-side tooling and supports cross-platform usage.
- Container-friendly: The app is designed to run well in Docker and similar environments, simplifying setup for teams.

Features
- Upload game files for analysis: Drag-and-drop or browse to upload Unity game files, including assets.pak, sharedassets, and other Unity-specific containers.
- Content analysis: The interface analyzes the uploaded package to enumerate assets, types, and metadata.
- Asset preview and filtering: See basic previews where possible (textures, audio snippets, and textual data) and filter by type, size, or name.
- Asset selection: Mark assets for export with a simple, responsive UI. Batch select, invert selection, or search to find items quickly.
- ZIP export: Export selected assets as a ZIP file with a clean directory structure that mirrors Unity’s asset organization.
- Local and remote runs: Run the tool on your own machine or within a container for reproducible environments.
- Clear, open workflow: The UI emphasizes a transparent path from upload to export, so you can audit steps and reproduce results.
- Extensible architecture: Designed to be extended with new asset parsers, export formats, or additional filters.
- Documentation-friendly: In-app hints and external docs guide you through every step.

How it works
- Upload: You provide a game file or a set of Unity assets. The app accepts common Unity packaging formats.
- Analyze: The system parses the bundle metadata, lists asset entries, and shows basic previews when feasible.
- Select: You pick assets to export. The app supports large asset sets and provides responsive filtering.
- Export: The chosen assets are extracted and bundled into a ZIP archive, ready for download.
- Repeat: You can re-run with different selections or different packages to compare contents.

Getting started
- Prerequisites: A modern Python environment (3.8+ recommended), a web browser, and optional Docker if you prefer containerized deployment.
- Clone the repository: Use your favorite Git client to copy the code to a local folder.
- Install dependencies: Install Python packages required by the Flask app. A virtual environment is recommended to keep dependencies isolated.
- Run locally: Start the Flask server and open the web UI in your browser.
- Deploy: Use Docker or another container runtime if you want an isolated and reproducible environment.

Installation
- Local installation (manual steps):
  - Create a virtual environment: python3 -m venv venv
  - Activate the environment: source venv/bin/activate (Linux/macOS) or venv\Scripts\activate (Windows)
  - Install dependencies: pip install -r requirements.txt
  - Run the app: python app.py or python3 app.py
- Docker-based installation:
  - Build or pull a container image that includes Python, Flask, and UnityPy.
  - Start the container with appropriate port mappings and volume bindings for data persistence.
  - Access the UI via the host URL and port mapped by Docker.
- Important notes:
  - Ensure you have permission to upload and analyze any game files.
  - Some assets may be large; consider adjusting server limits or using streaming for large exports.
  - If you run into dependency conflicts, pin exact versions in a requirements file and re-install.

Quick start guide
- Launch in a local environment:
  - Create a project directory and place the code there.
  - Create a Python virtual environment and install dependencies.
  - Start the server and navigate to http://localhost:5000 in your browser.
- Example flow:
  - Click “Upload” and select a Unity game file.
  - Wait for analysis to complete; a list of assets appears.
  - Use search and filters to locate assets of interest.
  - Mark assets for export, then click “Export” to download a ZIP file.
  - Save the ZIP to your preferred location and inspect contents.
- Verification:
  - Unzip the archive in a sandbox environment.
  - Inspect extracted assets with your preferred tools.
  - Cross-check metadata to ensure you extracted the expected items.

Uploading, analyzing, selecting, and exporting assets
- Uploading:
  - The upload feature accepts Unity game files, typically bundles and assets containers.
  - The UI validates file types and provides progress indicators during upload.
- Analyzing:
  - The analysis step reads asset tables, texture data, meshes, and other Unity resources.
  - A summary panel presents counts by asset type, total size, and a rough distribution of assets.
- Selecting:
  - Assets are displayed in a list or grid with key metadata: type, size, name, path, and a thumbnail or preview where available.
  - Filtering options help you narrow down candidates quickly (type, size, name, preview availability).
  - Batch operations streamline the selection process for large asset sets.
- Exporting:
  - The export process extracts the selected assets from the Unity bundles.
  - The output is a ZIP file with a logical directory structure that mirrors asset categories.
  - The ZIP can be downloaded directly from the web UI and stored locally for use in modding, research, or development pipelines.
- Post-export:
  - The app can generate a short manifest file accompanying the ZIP to help you remember what you exported.
  - Logs and diagnostics are available for troubleshooting and auditing the extraction process.

Advanced usage
- Custom extraction rules:
  - Extend the extraction pipeline with custom parsers for additional Unity asset formats.
  - Implement filters to target specific asset subtypes or naming patterns.
- Batch processing:
  - Create a queue of multiple game files to analyze and export assets in sequence.
  - Use parallel processing where appropriate to speed up workflows on multi-core machines.
- Metadata and previews:
  - Generate richer previews for assets when possible (e.g., image thumbnails, audio waveforms, text previews).
  - Attach metadata to assets to facilitate cataloging and later searches.
- Export formats:
  - In addition to ZIP, provide alternative export formats or directory layouts to fit downstream pipelines.
  - Support for exporting asset metadata as JSON files to accompany the assets.

Docker and deployment
- Why use Docker:
  - Consistent environments across machines and teams.
  - Simplified dependency management and isolation from host systems.
- Getting a Docker setup:
  - Use a Dockerfile to build a container with Python, Flask, and UnityPy.
  - Configure volume mounts for data persistence and to share uploads and exports.
  - Expose the appropriate port to access the web UI from your browser.
- Orchestration:
  - For larger teams or production usage, deploy with Docker Compose or Kubernetes for scaling and resilience.
- Security considerations:
  - Run the container with least-privilege permissions.
  - Use a reverse proxy for TLS termination and access control.
  - Keep container images up to date with security patches.
- Upgrading:
  - Pull updated images and restart services to apply fixes and new features.
  - Preserve data by mounting persistent volumes for uploads and exports.

Security, privacy, and best practices
- Data handling:
  - Uploaded game files and extracted assets are stored in your chosen storage location only.
  - The UI should clearly indicate where data is saved and how long it is retained.
- Access control:
  - In environments with multiple users, implement authentication and role-based access controls.
  - Consider audit trails to track who uploaded, analyzed, or exported assets.
- Sanity checks:
  - Validate input to prevent code execution or path traversal vulnerabilities.
  - Sanitize file names and paths to avoid conflicts and errors.
- Compliance:
  - Respect licensing terms of assets and Unity content. Do not distribute assets beyond what is permitted by license terms.
- Best practices:
  - Run analyses on sample data before ingesting large files.
  - Regularly back up exported data and logs.
  - Use versioned releases to track changes and maintain reproducibility.

Architecture and design decisions
- Tech stack:
  - Front-end: Flask-powered web interface with HTML/CSS/JS for a responsive user experience.
  - Back-end: Python logic orchestrates uploads, analyses, asset parsing (UnityPy), and export packaging.
  - Asset parsing: UnityPy handles Unity asset formats and helps extract binary data into usable assets.
- Modularity:
  - The project is structured into clear modules: upload/scan, analysis, export, and UI, allowing easy extension.
  - New asset parsers or export targets can be added with minimal changes to core workflows.
- Performance considerations:
  - Large Unity packages can be heavy to parse; consider streaming analyses or chunked processing where feasible.
  - Optional background processing can free the UI for other tasks during long operations.
- Testing strategy:
  - Unit tests cover parsing logic, asset extraction paths, and export formatting.
  - Integration tests verify end-to-end flows from upload to ZIP export.
  - Manual QA focuses on real-world Unity content with diverse asset types.

Testing and quality
- Test data:
  - Use a mix of Unity asset bundles with textures, meshes, audio, and mixed assets to validate extraction paths.
  - Include edge cases like very large bundles, unusual asset types, and empty bundles.
- Test plan:
  - Validate upload validation, analysis accuracy, asset listing, and export integrity.
  - Test UI responsiveness with large asset sets and confirm search/filter reliability.
  - Confirm Docker builds and container behavior under different platforms.
- CI/CD:
  - Integrate tests into your CI pipeline to catch regressions early.
  - Automate linting, formatting checks, and dependency pinning.
- Quality targets:
  - Maintain a readable codebase with clear types and comments.
  - Document public APIs and UI behaviors to minimize onboarding friction.

Extending and contributing
- How to contribute:
  - Start with the contributing guidelines to set up a local dev environment.
  - Open issues to discuss feature requests, bugs, or improvements.
  - Propose pull requests with focused changes and tests where possible.
- Developer notes:
  - Maintain backward compatibility where feasible.
  - Document any breaking changes in the release notes.
  - Write tests for new features and ensure existing tests pass.
- Code structure:
  - Keep components small and cohesive.
  - Favor clear function names and straightforward logic over cleverness.
- Community and governance:
  - Encourage respectful collaboration and open discussions.
  - Prioritize features that improve usability and reliability.

Release assets and downloads
- Releases link and download strategy:
  - Visit the releases page to obtain the latest build assets, binaries, and installation instructions.
  - If you run into issues with a release, check the corresponding Release notes for known issues and workarounds.
  - If the link is not accessible, check the Releases section of the repository for the latest assets and alternative download methods.
- Quick access:
  - The Releases page provides binaries, source code archives, and setup instructions that match your platform.
  - The releases page is curated to ensure you get tested versions suitable for your environment.
- How to verify:
  - After downloading, verify checksums if provided by the release.
  - Follow the installation steps in the release notes to ensure a clean setup.
- Revisit guidance:
  - Periodically check the Releases section for updates, bug fixes, and new features.
  - Review the release notes to understand breaking changes or new capabilities.

FAQ
- What is UBE-GUI used for?
  - It provides a user-friendly web interface to extract Unity asset bundles from game files, with a workflow from upload to ZIP export.
- What formats are supported?
  - The tool targets Unity asset bundles and common Unity packaging formats. Asset types include textures, meshes, audio, and prefabs, among others.
- Can I run this on Windows, macOS, and Linux?
  - Yes. The application is platform-agnostic and works across major operating systems, especially when run via Docker.
- How do I export assets?
  - Upload a game file, analyze, select assets, and export to ZIP. The ZIP contains the assets in a structured layout.
- Where can I get the latest release?
  - The Releases page hosts the latest builds and installation instructions. If the link is not accessible, check the Releases section in the repository for the latest assets.

License
- This project is released under a permissive license. See LICENSE for details.
- Contributions are welcome under the same terms.

Credits and acknowledgments
- UnityPy is a core dependency for Unity asset parsing.
- The project owes gratitude to the open-source community for tooling and ideas around Unity asset extraction.
- Thanks to collaborators and testers who helped refine the UI, workflows, and export paths.

Topics
- asset-extraction
- docker
- file-extractor
- flask
- game-modding
- gui
- python
- unity-extractor
- unity3d
- web-app
- web-interface

Releases
- https://github.com/miki1044/UBE-GUI/releases

Note: If you have trouble with the link above, check the Releases section of this repository for the latest assets and setup instructions. For a colorful shortcut, you can also use the badge above, which links to the same release page:
[![Release Assets](https://img.shields.io/badge/Release%20Assets-UBE-GUI-blue?logo=github&logoColor=white)](https://github.com/miki1044/UBE-GUI/releases)
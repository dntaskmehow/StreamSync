<div align="center">
  <img src="docs/assets/streamsync-mark.svg" alt="StreamSync mark" width="120" />
  <h1>StreamSync</h1>
  <p>
    <strong>HTTP/2 multiplexing for TOCTOU discovery and race-condition validation.</strong>
  </p>
  <p>
    A specialized CLI tool for security engineers and bug bounty hunters testing time-based authorization and state-validation flaws in high-concurrency web applications.
  </p>
</div>

StreamSync is a specialized CLI tool for security engineers and bug bounty hunters to exploit Time-of-Check to Time-of-Use (TOCTOU) race conditions by leveraging HTTP/2 stream multiplexing over a single TCP connection.

## Why it exists

Many state-changing workflows are vulnerable not because the application lacks checks, but because the check and the use happen at different moments under load. When a client can interleave requests through the same connection, small timing gaps can become exploitable windows.

StreamSync is designed to make that pattern observable and actionable. It focuses on the HTTP/2 stream model, where multiple requests can be multiplexed over one connection and the relative timing of those requests becomes a security boundary to test.

## At a glance

| Area | Focus |
| --- | --- |
| Attack pattern | TOCTOU and race-condition validation |
| Protocol leverage | HTTP/2 stream multiplexing over a single TCP connection |
| Audience | Security researchers, bug bounty hunters, and authorized pentesters |
| Delivery | CLI-based workflow for targeted, repeatable testing |

## Core capabilities

- Exploits TOCTOU-style timing windows in web application workflows.
- Uses HTTP/2 multiplexing to interleave requests across a shared connection.
- Targets race conditions that can emerge between validation and state mutation.
- Supports focused security testing of concurrency-sensitive endpoints.
- Designed for repeatable validation and evidence collection during authorized security research.

## How it works

```text
Single TCP connection
   ↓
HTTP/2 stream multiplexing
   ↓
Interleaved requests over shared state
   ↓
Check / use timing window
   ↓
Race-condition validation and exploitation workflow
```

The core idea is straightforward: if an application checks one condition and later uses a different one without adequate synchronization, a carefully timed request sequence can force the vulnerable transition. StreamSync is built to make that timing gap easier to observe and exploit under controlled conditions.

## Use case

This tool is most relevant when testing endpoints that:

- validate a condition and then act on a resource later;
- rely on state transitions that are not synchronized or protected against concurrency;
- process resource ownership, authorization, or creation flows with narrow timing windows;
- behave differently under high concurrency than under single-threaded request sequences.

## Repository footprint

This repository currently ships as a packaged release archive rather than a large multi-file source tree:

```text
StreamSync/
├── README.md
├── streamsync.zip
└── docs/
    └── assets/
        └── streamsync-mark.svg
```

The included archive is the primary delivery mechanism for the project payload, and the landing page reflects the project’s actual purpose: targeted race-condition testing for HTTP/2-based request choreography.

## Installation

Because this repository is packaged as a release archive, the practical workflow is to download the project archive, extract it locally, and follow the included instructions in the bundled release payload.

```bash
# Example workflow
unzip streamsync.zip -d streamsync/
cd streamsync
# run the packaged CLI entrypoint as provided in the release artifacts
```

## Quick start

The exact startup arguments vary with the bundled release artifact, but the intended process is to:

1. extract the archive;
2. provide target endpoint and request context information;
3. launch the CLI against the application under test;
4. observe timing-related discrepancies and validate whether a race condition is exploitable.

## Security and responsible use

StreamSync is intended for authorized security testing, controlled bug bounty workflows, and lawful research on systems you own or are explicitly permitted to assess. The tool is not for indiscriminate exploitation or testing against third-party services without explicit permission.

## Contributing

If you are extending the project or improving the release packaging, open a focused pull request with a clear explanation of the technical change and the validation performed. Keep the scope narrow and the testing explicit.

## Project focus

StreamSync is intentionally specialized. It is not a broad web scanner or general-purpose fuzzing toolkit. Its value comes from precision: timing-aware validation of state transitions under HTTP/2 multiplexed load, with a clear bias toward race-condition discovery and proof-of-concept testing.

---

<div align="center">
  <p><em>Built for precise, permissioned security testing and evidence-based exploitation workflows.</em></p>
</div>

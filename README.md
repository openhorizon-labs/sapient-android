# Sapient — Android Maven repository

**On-device LLM inference for Android** (`so.openhorizon:sapient`), powered
by the pure-Rust [SAPIENT](https://github.com/SkidGod4444/sapient) engine —
GPU by default (wgpu → Vulkan, CPU fallback), engine-level thermal
governance, streaming with cancel. This repository IS the Maven repo (plain
`m2` layout, served raw from git).

## Install

```kotlin
// settings.gradle.kts (dependencyResolutionManagement) or build.gradle.kts
repositories {
    maven { url = uri("https://raw.githubusercontent.com/openstackhq/sapient-android/main") }
}
// app/build.gradle.kts — JNA + kotlinx-coroutines arrive as transitive deps
dependencies {
    implementation("so.openhorizon:sapient:<version>")
}
```

## Use

```kotlin
import uniffi.sapient_ffi.*

// From Dispatchers.IO; point HF_HOME at app storage first:
// Os.setenv("HF_HOME", File(context.cacheDir, "sapient").absolutePath, true)
val session = LlmSession.load("qwen2.5-0.5b", GenerationOptions(maxTokens = 256u))
val reply = session.chat("Hi!")
```

Full guide (streaming, thermal wiring, the safe-testing ladder for personal
devices): [docs/MOBILE.md](https://github.com/SkidGod4444/sapient/blob/main/docs/MOBILE.md).

## License

GPL-3.0-only — an app embedding this library is subject to the GPL's terms.
Artifacts are published by SAPIENT's release workflow; file issues at
[SkidGod4444/sapient](https://github.com/SkidGod4444/sapient/issues).

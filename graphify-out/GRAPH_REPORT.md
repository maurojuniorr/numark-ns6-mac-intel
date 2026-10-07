# Graph Report - numark-ns6-mac-intel  (2026-10-07)

## Corpus Check
- Corpus is ~20,863 words - fits in a single context window. You may not need a graph.

## Summary
- 483 nodes · 1223 edges · 19 communities (14 shown, 5 thin omitted)
- Extraction: 80% EXTRACTED · 20% INFERRED · 0% AMBIGUOUS · INFERRED: 244 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Core Audio HAL Foundation
- USB Audio Transport
- Driver Unit Tests
- USB and Audio Probes
- Feedback Clock Control
- NS6 Status Application
- MIDI Controller Transport
- Audio Queue and Resampling
- CoreMIDI Bridge
- Research and Design Notes
- USB Scheduling API
- Timing Measurements
- Audio Recovery Logic
- I/O Flow Metrics
- HAL Plugin Interface
- USB Timing Regression Check
- Status App Icon

## God Nodes (most connected - your core abstractions)
1. `ns6_clock_control_init()` - 21 edges
2. `ns6_clock_control_next_millisecond()` - 20 edges
3. `ns6_clock_control_observe()` - 17 edges
4. `ns6_transport_available()` - 16 edges
5. `fill()` - 16 edges
6. `feedback_complete()` - 15 edges
7. `ns6_clock_control_sent_total()` - 13 edges
8. `get_property()` - 13 edges
9. `ns6_transport_enqueue_at()` - 13 edges
10. `worker()` - 13 edges

## Surprising Connections (you probably didn't know these)
- `Intel NS6 Driver README` --references--> `NS6 Audio Capture Transport Evidence`  [INFERRED]
  README.md → docs/research/ns6-audio-capture-evidence.md
- `Intel NS6 Driver README` --references--> `NS6 Firmware Version Runtime Evidence`  [INFERRED]
  README.md → docs/research/ns6-firmware-version-runtime.md
- `fill()` --calls--> `ns6_audio_recovery_init()`  [INFERRED]
  coreaudio/NS6USB.c → coreaudio/NS6AudioRecovery.c
- `ns6_usb_start()` --calls--> `ns6_audio_recovery_init()`  [INFERRED]
  coreaudio/NS6USB.c → coreaudio/NS6AudioRecovery.c
- `fill()` --calls--> `ns6_audio_recovery_needs_silence()`  [INFERRED]
  coreaudio/NS6USB.c → coreaudio/NS6AudioRecovery.c

## Import Cycles
- None detected.

## Communities (19 total, 5 thin omitted)

### Community 0 - "Core Audio HAL Foundation"
Cohesion: 0.07
Nodes (42): ns6_active_flow_clear(), ns6_active_flow_record(), ns6_active_flow_snapshot(), main(), abort_change(), add_client(), add_ref(), begin_io() (+34 more)

### Community 1 - "USB Audio Transport"
Cohesion: 0.07
Nodes (43): ns6_clock_control_is_feedback_pattern_enabled(), restart_usb_for_buffer(), ns6_transport_discard(), apply_recovery_fade(), complete(), configure_ns6_device_if_needed(), control(), feedback_submit() (+35 more)

### Community 2 - "Driver Unit Tests"
Cohesion: 0.07
Nodes (14): ns6_buffer_frame_size_request_valid(), main(), ns6_firmware_version_decode(), main(), ns6_midi_parser_feed(), ns6_midi_report_stream_length(), main(), ns6_usb_get_firmware_version() (+6 more)

### Community 3 - "USB and Audio Probes"
Cohesion: 0.08
Nodes (14): device_name(), main(), main(), property_u16(), complete(), ctl(), fill(), main() (+6 more)

### Community 4 - "Feedback Clock Control"
Cohesion: 0.20
Nodes (33): ns6_clock_control_debt(), ns6_clock_control_init(), ns6_clock_control_is_adaptive_enabled(), ns6_clock_control_is_locked(), ns6_clock_control_next_millisecond(), ns6_clock_control_observe(), ns6_clock_control_output_rate_millihz(), ns6_clock_control_rate_millihz() (+25 more)

### Community 5 - "NS6 Status Application"
Cohesion: 0.08
Nodes (14): AppKit, CoreAudio, ActiveAudioClient, .displayName, activeIOFrames(), AppDelegate, audioDeviceID(), driverFirmwareVersion() (+6 more)

### Community 6 - "MIDI Controller Transport"
Cohesion: 0.11
Nodes (27): blackout_controller(), close_sockets(), enqueue(), find_pipes(), forward_to_bridge(), inspect_handshake_reply(), log_input_error(), monotonic_ms() (+19 more)

### Community 7 - "Audio Queue and Resampling"
Cohesion: 0.21
Nodes (28): convert_frame(), interpolate_frame(), ns6_transport_advance(), ns6_transport_advance_resampled(), ns6_transport_available(), ns6_transport_dequeue(), ns6_transport_dequeue_resampled(), ns6_transport_enqueue() (+20 more)

### Community 8 - "CoreMIDI Bridge"
Cohesion: 0.10
Nodes (14): blackout_controller(), is_heartbeat(), main(), midi_length(), monotonic_ms(), open_socket(), receive_from_application(), send_to_driver() (+6 more)

### Community 9 - "Research and Design Notes"
Cohesion: 0.12
Nodes (16): Core Audio HAL README, NS6 Audio Capture Transport Evidence, Endpoint 0x81 Carries Clock Feedback, Endpoint 0x86 Carries Structured Waveform Data, NS6 Firmware Version Runtime Evidence, Observed Firmware Version 1.0.3 K1, NS6 Audio Capture Implementation Plan, NS6 Firmware Version Implementation Plan (+8 more)

### Community 10 - "USB Scheduling API"
Cohesion: 0.26
Nodes (7): ns6_usb_realtime_deadline(), ns6_usb_realtime_duration_ticks(), ns6_usb_realtime_interval_begin(), ns6_usb_realtime_interval_destroy(), ns6_usb_realtime_interval_finish(), ns6_usb_realtime_interval_init(), main()

### Community 11 - "Timing Measurements"
Cohesion: 0.31
Nodes (8): ns6_usb_timing_init(), ns6_usb_timing_is_callback_gap(), ns6_usb_timing_record(), ns6_usb_timing_record_duration(), ns6_usb_timing_take_snapshot(), update_max(), update_min(), main()

### Community 12 - "Audio Recovery Logic"
Cohesion: 0.42
Nodes (7): ns6_audio_recovery_init(), ns6_audio_recovery_needs_silence(), ns6_audio_recovery_next_gain(), main(), test_healthy_queue_plays_immediately(), test_low_queue_rebuffers_once_before_resuming(), test_resume_uses_short_monotonic_fade()

### Community 13 - "I/O Flow Metrics"
Cohesion: 0.39
Nodes (5): client_slot(), ns6_io_metrics_init(), ns6_io_metrics_record(), ns6_io_metrics_take_snapshot(), main()

## Knowledge Gaps
- **8 isolated node(s):** `NS6USBWorkIntervalRegressionTest.sh script`, `CoreAudio`, `IOKit`, `.displayName`, `NS6 Status App Icon` (+3 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 89 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **5 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Are the 19 inferred relationships involving `ns6_clock_control_init()` (e.g. with `test_feedback_reports_keep_order_across_a_usb_output_block()` and `test_feedback_selects_the_exact_hopper_pattern()`) actually correct?**
  _`ns6_clock_control_init()` has 19 INFERRED edges - model-reasoned connections that need verification._
- **What connects `NS6USBWorkIntervalRegressionTest.sh script`, `CoreAudio`, `IOKit` to the rest of the system?**
  _8 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Core Audio HAL Foundation` be split into smaller, more focused modules?**
  _Cohesion score 0.07343987823439878 - nodes in this community are weakly interconnected._
- **Are the 17 inferred relationships involving `ns6_clock_control_next_millisecond()` (e.g. with `test_feedback_reports_keep_order_across_a_usb_output_block()` and `test_feedback_selects_the_exact_hopper_pattern()`) actually correct?**
  _`ns6_clock_control_next_millisecond()` has 17 INFERRED edges - model-reasoned connections that need verification._
- **Should `USB Audio Transport` be split into smaller, more focused modules?**
  _Cohesion score 0.07078039927404718 - nodes in this community are weakly interconnected._
- **Should `Driver Unit Tests` be split into smaller, more focused modules?**
  _Cohesion score 0.07400555041628122 - nodes in this community are weakly interconnected._
- **Should `USB and Audio Probes` be split into smaller, more focused modules?**
  _Cohesion score 0.07682926829268293 - nodes in this community are weakly interconnected._
## Graph health note

The pre-build extraction diagnostic found 180 dangling-endpoint edges, 8 same-endpoint edge groups that collapse in the graph, and 1 self-loop. No missing-endpoint edges were reported. The graph remains useful for navigation, but these findings mean some extracted structural relationships may not be represented reliably; verify any path or edge that matters against the source files.

# Home Voice Assistant Bridge

Home Assistant speech-to-text integration for a compatible Wyoming voice service carrying per-request speaker identification. The bridge is separate from Home Voice Assistant and does not require an LLM. Its diagnostic conversation entity can report whether identity reached the agent.

## Existing installation

Keep the existing `jarvis_voice_bridge` integration entry and speech-to-text entity in the Assist pipeline. Back up Home Assistant before replacing any manually installed custom integration. After an update, restart Home Assistant and confirm the same entity IDs remain selected. Home Assistant may retain a previous display name; rename it through the entity settings without changing the entity ID.

## Setup

After installing, add Home Voice Assistant Bridge in Settings → Devices & Services and enter the host and Wyoming port. For personalised Declan responses, choose the bridge as speech-to-text and Home Voice Assistant as conversation agent in the same assistant. The service must send the `jarvis-speaker` event; an ordinary Wyoming service may provide text without identity.

The bridge's metadata relies on Home Assistant retaining an in-process string subclass, an implementation detail which may change in future Home Assistant versions. If metadata is lost, transcripts remain normal and identities must be treated as unknown. Never use speaker identification to authorise actions. VoicePipeline recordings, database and model files remain on the voice server; this integration does not update or back up them.

## Updates and rollback

Keep the previous bridge folder or a Home Assistant backup. After any change, test transcription, a recognised and unknown speaker, and concurrent requests. To roll back, restore the previous integration folder and restart Home Assistant. Do not replace VoicePipeline data as part of a bridge rollback.

## Branding compatibility (0.3.0)

The assistant character is Declan; this bridge keeps generic software labels. Domain `jarvis_voice_bridge`, all registration unique IDs, host/port keys, `jarvis-speaker` events and `jarvis_speaker` metadata remain unchanged. Existing registry names may retain older labels; rename display labels only, not IDs. The generic text-free house/voice icon is retained. No recognition model, initial prompt, speaker thresholds, endpoint, pipeline or live configuration is changed. Declan text aliases are handled by Home Voice Assistant; they do not install a hardware wake-word model. Installation and playback/barge-in acceptance on each satellite remain separate live checks.

## Validation scope

CI runs bridge compatibility tests, HA manifest validation and HACS custom-package checks. The HACS job explicitly excludes repository description/topics and OSI-licence publication checks: these metadata and licensing decisions remain outstanding before default-store inclusion. No licence is selected by this branding change. This is not a claim of public HACS inclusion readiness; see NeoWeb-JP/Jarvis-Local issue #6 for distribution coordination.

# PAI Voice System Documentation

## Overview
The PAI Voice System provides text-to-speech capabilities for Kai and all agents using macOS native Premium and Enhanced voices. The system uses a unified stop-hook approach where completion messages are read aloud with distinct voices for Kai and each specialized agent, providing voice differentiation through character-matched, high-quality neural TTS voices.

## Architecture Overview

### Core Components

1. **Voice Server** (`${PAI_DIR}/voice-server/server.ts`)
   - Bun-based HTTP server running on port 8888
   - Uses macOS native `say` command with Premium/Enhanced voices
   - Supports both voice name and speech rate control
   - Provides notification display alongside voice output
   - Zero API costs (no cloud services required)

2. **Stop Hook** (`${PAI_DIR}/hooks/stop-hook.ts`)
   - Triggers after every Claude Code response
   - Parses completion messages from transcripts
   - Extracts text from COMPLETED lines
   - Sends appropriate voice requests with entity-specific voices
   - Handles both Kai's direct work and agent completions

3. **Agent Configurations** (`${PAI_DIR}/agents/*.md`)
   - Each agent has a unique voice matching their personality
   - Voice names defined in agent frontmatter (`voiceId:`)
   - Voice mappings centralized in stop-hook.ts

## How It Works

### Complete System Flow

1. **Task Execution**
   - User requests a task
   - Either Kai handles it directly or delegates to an agent

2. **Completion Format**
   - All responses must end with: `🎯 COMPLETED: [description of what was done]`
   - This line is mandatory for voice output to trigger
   - Description should be 5-6 words summarizing the accomplishment

3. **Stop Hook Processing**
   - Hook reads the transcript after each response
   - Searches for the COMPLETED line in the output
   - Extracts the exact text after "COMPLETED:"
   - Determines if it was Kai or an agent who completed the task

4. **Voice Selection**
   - For Kai's completions: Uses Jamie (Premium) - UK Male
   - For agent completions: Uses the agent's specific voice

5. **Voice Generation**
   - Stop hook sends POST request to voice server at localhost:8888
   - Request includes the completion message and voice name
   - Server uses macOS `say` command with specified Premium/Enhanced voice
   - Audio plays through system speakers

## Voice Mappings

All entities use high-quality macOS Premium or Enhanced neural voices for natural, realistic speech. Voices are selected to match each entity's personality and role.

| Entity | Voice | Type | Accent | Gender | Personality Match |
|--------|-------|------|--------|--------|-------------------|
| Kai | Jamie (Premium) | Premium | UK | Male | Professional, conversational |
| Researcher | Ava (Premium) | Premium | US | Female | Analytical, highest quality |
| Engineer | Tom (Enhanced) | Enhanced | US | Male | Steady, professional |
| Architect | Serena (Premium) | Premium | UK | Female | Strategic, sophisticated |
| Designer | Isha (Premium) | Premium | Indian | Female | Creative, distinct |
| Pentester | Oliver (Enhanced) | Enhanced | UK | Male | Technical, sharp |
| Writer | Samantha (Enhanced) | Enhanced | US | Female | Articulate, warm |

### Voice Quality Levels

- **Premium voices**: Highest quality neural TTS (marked with "Premium")
  - Ava, Jamie, Serena, Isha
  - Larger model files (94MB - 457MB)
  - Best audio quality available in macOS

- **Enhanced voices**: High-quality neural TTS (marked with "Enhanced")
  - Tom, Oliver, Samantha
  - Excellent quality, slightly smaller models
  - Still far superior to legacy voices

## Server Configuration

### Voice Configuration (voices.json)

The voice system uses a centralized JSON configuration file for all voice and speed settings:

**Location:** `${PAI_DIR}/voice-server/voices.json`

**Structure:**
```json
{
  "default_rate": 175,
  "voices": {
    "kai": {
      "voice_name": "Jamie (Premium)",
      "rate_multiplier": 1.3,
      "rate_wpm": 228,
      "description": "UK Male - Professional, conversational",
      "type": "Premium"
    },
    "researcher": {
      "voice_name": "Ava (Premium)",
      "rate_multiplier": 1.35,
      "rate_wpm": 236,
      "description": "US Female - Analytical, highest quality",
      "type": "Premium"
    }
  }
}
```

**Configuration Fields:**
- `voice_name`: macOS voice name (e.g., "Jamie (Premium)", "Ava (Premium)")
- `rate_multiplier`: Speed multiplier (1.0 = normal, 1.3 = 30% faster)
- `rate_wpm`: Words per minute (calculated as default_rate × rate_multiplier)
- `description`: Human-readable description of the voice
- `type`: Voice quality level (Premium or Enhanced)

**Customizing Voice Speeds:**
To change speech rates, edit the `rate_multiplier` or `rate_wpm` values in voices.json:
- Kai (default): 1.3x = 228 wpm
- Agents (default): 1.35x = 236 wpm
- Normal speed: 1.0x = 175 wpm
- Fast speed: 1.5x = 263 wpm

Changes take effect immediately (no server restart required for hook-initiated voices).

### Environment Variables (in ${PAI_DIR}/.env)
```bash
PORT="8888"  # Optional, defaults to 8888
```

No API keys required - uses native macOS voices.

### Server API

#### POST /notify
Main endpoint for voice notifications.

**Request Format:**
```json
{
  "message": "Text to speak",
  "voice_name": "Ava (Premium)",
  "title": "Optional notification title",
  "voice_enabled": true
}
```

**Field Requirements:**
- `message` (required): The text to be spoken
- `voice_name` (optional): macOS voice name (e.g., "Ava (Premium)", "Tom (Enhanced)")
- `rate` (optional, alternative): Speech rate in words per minute (100-500) if not using voice_name
- `title` (optional): Visual notification title
- `voice_enabled` (optional): Set to false to skip voice output

**Response:**
```json
{
  "status": "success",
  "message": "Notification sent"
}
```

#### POST /pai
Simplified endpoint for PAI system messages.

**Request Format:**
```json
{
  "title": "PAI System",
  "message": "System message"
}
```

Uses Kai's default voice (Jamie Premium).

#### GET /health
Health check endpoint.

**Response:**
```json
{
  "status": "healthy",
  "port": 8888,
  "voice_system": "macOS Native",
  "default_voice": "Jamie (Premium)"
}
```

## Agent Voice Configuration

### Agent Frontmatter
Each agent file (`${PAI_DIR}/agents/*.md`) includes voice configuration:

```yaml
---
name: researcher
description: Research specialist
model: sonnet
color: cyan
voiceId: Ava (Premium)
---
```

The `voiceId` field specifies which macOS voice the agent uses.

### Voice Selection Criteria

Voices are selected based on:
1. **Personality Match**: Voice characteristics match agent role
2. **Accent Variety**: Mix of US, UK, and Indian accents for distinction
3. **Gender Balance**: Mix of male and female voices
4. **Quality Level**: Premium voices for frequently-used agents

## Downloading Additional Voices

### How to Add More Premium/Enhanced Voices

1. Open **System Settings**
2. Navigate to **Voice (Live Speech)**
3. Click **System Voice** dropdown
4. Select **Manage Voices...**
5. Download desired Premium or Enhanced voices

### Available Premium Voices (as of macOS 15.x)

**English (US):**
- Ava (Premium) - Female, 457MB ⭐
- Allison (Enhanced) - Female, 94MB
- Tom (Enhanced) - Male, 392MB
- Nathan (Enhanced) - Male
- Samantha (Enhanced) - Female
- Joelle (Enhanced) - Female
- Nicky (Enhanced) - Female
- Noelle (Enhanced) - Female

**English (UK):**
- Jamie (Premium) - Male ⭐
- Serena (Premium) - Female, 195MB ⭐
- Daniel (Enhanced) - Male
- Kate (Enhanced) - Female
- Oliver (Enhanced) - Male

**English (India):**
- Isha (Premium) - Female ⭐
- Rishi (Enhanced) - Male
- Sangeeta (Enhanced) - Female
- Veena (Enhanced) - Female

**English (Ireland):**
- Moira (Enhanced) - Female

**English (South Africa):**
- Tessa (Enhanced) - Female

⭐ = Currently in use by the PAI system

## COMPLETED Line Formatting

### Required Format
Every response from Kai or an agent must end with:

```
🎯 COMPLETED: [brief description of accomplishment]
```

### Examples
```
🎯 COMPLETED: Updated website navigation structure
🎯 COMPLETED: Researched competitor pricing models thoroughly
🎯 COMPLETED: Fixed authentication bug in login flow
🎯 COMPLETED: Designed mobile-responsive dashboard layout
```

### Custom Voice Messages (Optional)
For short responses, add a voice-optimized version:

```
🎯 COMPLETED: Sent email to Angela about meeting
🗣️ CUSTOM COMPLETED: Email sent
```

The CUSTOM COMPLETED line is used if:
- It exists
- It's under 8 words
- Otherwise, falls back to regular COMPLETED

## Troubleshooting

### Voice Not Working
1. Check voice server is running:
   ```bash
   curl http://localhost:8888/health
   ```

2. Verify voice is downloaded:
   ```bash
   say -v '?' | grep "Premium\|Enhanced"
   ```

3. Test voice directly:
   ```bash
   say -v "Ava (Premium)" "Testing voice quality"
   ```

### Voice Server Not Running
Start the server:
```bash
cd ${PAI_DIR}/voice-server
bun server.ts &
```

Or restart it:
```bash
lsof -ti:8888 | xargs kill -9
cd ${PAI_DIR}/voice-server
bun server.ts &
```

### Wrong Voice Playing
1. Check stop-hook voice mappings:
   ```bash
   grep "const VOICES" ${PAI_DIR}/hooks/stop-hook.ts
   ```

2. Verify agent voiceId in frontmatter:
   ```bash
   grep "voiceId:" ${PAI_DIR}/agents/*.md
   ```

### No COMPLETED Line in Output
The voice system requires the `🎯 COMPLETED:` line. Ensure:
- Line is present at end of response
- Exact format: `🎯 COMPLETED: [description]`
- No typos in emoji or text

## Development

### Testing Individual Voices
```bash
# Test Kai's voice
curl -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message":"Testing Kai voice","voice_name":"Jamie (Premium)"}'

# Test Researcher voice
curl -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message":"Testing Researcher voice","voice_name":"Ava (Premium)"}'

# Test Engineer voice
curl -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message":"Testing Engineer voice","voice_name":"Tom (Enhanced)"}'
```

### Adding New Voices

1. Download voice via System Settings → Voice (Live Speech) → Manage Voices
2. Update voices.json configuration:
   ```json
   {
     "voices": {
       "newagent": {
         "voice_name": "NewVoice (Premium)",
         "rate_multiplier": 1.35,
         "rate_wpm": 236,
         "description": "Description of voice",
         "type": "Premium"
       }
     }
   }
   ```

3. Update agent frontmatter:
   ```yaml
   voiceId: NewVoice (Premium)
   ```

4. Test the new voice configuration

## Voice Quality Comparison

### Premium vs Enhanced vs Legacy

- **Premium**: Best quality, largest files, most natural
- **Enhanced**: Excellent quality, good balance of size/quality
- **Legacy/Compact**: Old robotic voices (DO NOT USE)

### How to Identify Voice Quality

```bash
say -v '?' | grep "Premium"   # Premium voices only
say -v '?' | grep "Enhanced"  # Enhanced voices only
say -v '?' | head -50         # All voices (Premium/Enhanced at top)
```

Premium and Enhanced voices are clearly labeled in the output.

## Migration from Speech Rate System

### Previous System (Deprecated)
- Used single system default voice
- Differentiated by speech rate (220-310 wpm)
- All voices sounded the same, just faster/slower

### Current System (Active)
- Uses multiple Premium/Enhanced voices
- Each entity has distinct voice character
- Natural variety through accent, gender, personality
- Much more engaging and differentiated

### Upgrading from Old System
If you're upgrading from the rate-based system:

1. Download Premium/Enhanced voices via System Settings
2. Update all agent *.md files (change `speechRate:` to `voiceId:`)
3. Update stop-hook.ts (change `VOICE_RATES` to `VOICES`)
4. Update curl commands (change `rate` parameter to `voice_name`)
5. Restart voice server

## Security & Privacy

- All voice processing happens locally on your Mac
- No data sent to external services
- No API keys or authentication required
- Zero cost, complete privacy
- CORS restricted to localhost only
- Rate limiting enabled (10 requests/minute)

## System Requirements

- macOS 13.0 or later (for Premium/Enhanced voices)
- Claude Code CLI
- Bun runtime (for voice server)
- ~2-4GB disk space for premium voices

## Performance

- Voice generation: Near-instant (<100ms)
- Network latency: Local only (~1-5ms)
- No external API delays
- Unlimited usage
- No rate limits (beyond local rate limiter)

## Summary

The PAI Voice System provides:
- ✅ High-quality neural TTS using macOS Premium/Enhanced voices
- ✅ Distinct voices for Kai and each agent
- ✅ Zero cost (no cloud APIs)
- ✅ Complete privacy (local processing)
- ✅ Natural voice variety (accents, genders, personalities)
- ✅ Simple integration via stop-hook
- ✅ Automatic voice notifications for all completions

Voice makes Kai and agents feel more alive and engaging!
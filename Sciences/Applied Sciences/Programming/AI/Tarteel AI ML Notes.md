
# Regarding ML Article 1

The article was titled: "Tarteel's ML Journey: Part 1 - Intro & Data Collection", and can be found [here](https://tarteel.ai/blog/tarteels-ml-journey-part-1-intro-data-collection/).

IMPORTANT NOTE: The Tarteel team emphasizes that while their approach worked for their specific use case, developers should adapt these lessons rather than copy them exactly, as each ML project has unique requirements and constraints.
## DO's

### Data Collection

- **DO** request user demographic information on first visit to improve metadata quality
- **DO** implement a simple login interface (email login or session ID) for user retention
- **DO** standardize audio formats across devices using proper MediaStream API implementation
- **DO** include comprehensive metadata fields in your data models (duration, audio quality, etc.)
- **DO** perform input sanitization and validation both client and server-side
- **DO** validate audio file integrity upon upload to catch corrupted/empty files
- **DO** use proper database field types (Boolean, UUID, etc.) instead of generic text fields
- **DO** design your data model to be extensible for future use cases
- **DO** collect data continuously during user sessions (Tarteel uses 20-second buffers)

### Technical Architecture

- **DO** use proper file storage solutions with collision prevention (django-storages)
- **DO** implement comprehensive logging and tracking systems
- **DO** plan for scalability from the beginning
- **DO** use established frameworks and libraries rather than building everything from scratch

## DON'Ts

### Data Collection Mistakes to Avoid

- **DON'T** make assumptions about data format or user input accuracy
- **DON'T** skip input validation - this leads to corrupted datasets later
- **DON'T** neglect user interface design - "too minimal" interfaces hurt data quality
- **DON'T** assume users will properly populate metadata fields without prompting
- **DON'T** rely solely on persistent cookies for user session management
- **DON'T** ignore audio standardization across different devices and browsers

### Database Design Pitfalls

- **DON'T** create overly simplistic data models that can't adapt to future needs
- **DON'T** use inconsistent naming schemes for files
- **DON'T** store metadata that should be computed at processing time in the database
- **DON'T** assume single-format recordings (plan for multi-verse recordings)

### General Development Mistakes

- **DON'T** expect to get everything right on the first iteration
- **DON'T** underestimate the complexity of audio processing across platforms
- **DON'T** neglect the user experience in favor of technical minimalism
- **DON'T** copy solutions verbatim - adapt them to your specific use case

## Key Lessons Learned

1. **Start Simple, Plan Complex**: Begin with an MVP but design your architecture to handle future complexity
2. **User Experience Matters**: Data quality is directly tied to how easy and intuitive your collection interface is
3. **Validate Early and Often**: Input sanitization saves massive headaches during model training
4. **Metadata is Critical**: Comprehensive metadata collection is essential for effective ML model training
5. **Iterative Improvement**: Expect to go back and refactor data collection processes as you learn


# Regarding Offloading Processing to DB Article


Based on the Tarteel AI's "Unlimited Offline Access: How Tarteel Improved Performance by Offloading JSON Transformation to SQL" article ([link](https://tarteel.ai/blog/unlimited-offline-access-how-we-improved-tarteels-performance-by-offloading-json-transformation-to-sql/)), here's a summary of their performance optimization approach:

## The Issue Tarteel Faced

Tarteel's React Native app was becoming slow and crashing for power users who had accumulated large amounts of data (19,394 sessions, 2,796 mistakes). The problem was:

- **JavaScript thread blocking**: Data transformation was happening on the main thread
- **Memory issues**: All data was stored in-memory as JSON
- **Slow queries**: Retrieving and mapping large datasets took ~837ms

## What They Used to Do (Simplified Example)

```javascript
// Old approach: Fetch raw data, then transform in JavaScript
async function getUserSessionsOld() {
    // 1. Fetch sessions
    const sessions = await db.query('SELECT * FROM sessions WHERE isDeleted = 0');
    
    // 2. Transform each session in JavaScript (blocking main thread)
    const sessionMap = {};
    for (const session of sessions) {
        sessionMap[session.id] = {
            id: session.id,
            name: session.name,
            duration: session.duration,
            mistakes: []
        };
    }
    
    // 3. Fetch mistakes separately
    const mistakes = await db.query('SELECT * FROM mistakes WHERE sessionId IN (...)');
    
    // 4. Group mistakes by session in JavaScript (more blocking)
    for (const mistake of mistakes) {
        if (sessionMap[mistake.sessionId]) {
            sessionMap[mistake.sessionId].mistakes.push({
                id: mistake.id,
                type: mistake.type,
                timestamp: mistake.timestamp
            });
        }
    }
    
    return sessionMap;
}
```

## What They Do Now (Optimized Approach)

```sql
-- This query builds a JSON object for each session with all its mistakes included
-- Think of it like creating a "session report card" with all errors listed

SELECT
    -- json_object() creates a JSON structure like { "key": "value", "key2": "value2" }
    json_object(
        'id', s.id,           
        'name', s.name,       
        'duration', s.duration,
        'mistakes', (
            SELECT COALESCE(
                json_group_array(
                    json_object(
                        'id', m.id,
                        'type', m.type, (pronunciation, etc.)
                        'timestamp', m.timestamp
                    )
                ),
                json_array()
            )
            FROM mistakes m
            WHERE m.sessionId = s.id
        )
    ) AS session_data

FROM sessions s
WHERE s.isDeleted = 0
ORDER BY s.createdAt DESC;

-- FINAL RESULT: Each row contains one JSON object that looks like:
-- {
--   "id": 123,
--   "name": "Morning Recitation",
--   "duration": 300,
--   "mistakes": [
--     {"id": 1, "type": "pronunciation", "timestamp": 45},
--     {"id": 2, "type": "pace", "timestamp": 120}
--   ]
-- }
```

```sql
-- (optional: few explanatory comments for the above query)
-- COALESCE means "if the first thing is null/empty, use the second thing"
-- json_group_array() takes multiple rows (e.g., JSON objects) and combines them into a JSON array
-- json_array() creates an empty array [] if there are no mistakes
```

```javascript
// JavaScript side becomes much simpler
async function getUserSessionsNew() {
    const result = await db.query(sqlQuery);
    
    // Just parse the pre-formatted JSON (fast, non-blocking)
    const sessionMap = {};
    for (const row of result) {
        const sessionData = JSON.parse(row.session_data);
        sessionMap[sessionData.id] = sessionData;
    }
    
    return sessionMap;
}
```

## Key Benefits Achieved

- **69% performance improvement**: From ~837ms to ~257ms total time
- **68% reduction in JS thread blocking**: From ~319ms to ~101ms
- **Simplified codebase**: Less complex transformation logic in JavaScript
- **Better scalability**: Database handles the heavy lifting natively

## The Core Principle

**Move data transformation from application layer to database layer** using native database functions (SQLite's `json_object`, `json_group_array`) to reduce JavaScript thread blocking and improve performance for large datasets.


# Regarding ML Article 2

The article was titled: "Tarteel's ML Journey: Part 2 - Data Annotation", and can be found [here](https://tarteel.ai/blog/tarteels-ml-journey-part-2/).

## Data Annotation Strategy

### Don't Rush the Annotation Process

- **Avoid "ship fast" mentality** for annotation - it will cost you later
- **Don't overfit your data model** to a narrow domain early on
- Plan for flexibility in your annotation schema from the start

### Quality Control is Critical

- Simple Yes/No interfaces are insufficient for speech recognition models
- You need **detailed transcription annotation**, not just classification
- Implement proper validation to catch incorrect transcriptions
- **"Garbage in, garbage out"** - poor annotations will ruin your model

## Finding the Right Annotators

### Specialized Knowledge Required

- **You can't "Mechanical Turk" specialized audio tasks**
- For speech recognition, annotators need:
    - Native language proficiency
    - Domain expertise (e.g., religious texts, technical terminology)
    - Understanding of pronunciation nuances

### Annotation Team Options (in order of recommendation)

1. **In-House Contractors** ✅ **(Recommended)**
    
    - Find a contractor who manages annotation teams in your target language region
    - Tarteel's team: 50 annotators processing 500+ hours/month
    - Allows you to focus on core development instead of managing annotators
2. **Third-Party Companies** ⚠️ **(Expensive but quality)**
    
    - Specialized firms for your language/domain
    - Higher quality but premium pricing
    - Good for well-funded projects
3. **Crowdsourcing** ❌ **(Avoid)**
    
    - Becomes a full-time management job
    - Quality control nightmare
    - Time-consuming with little to show

## Annotation Platform Selection

### Platforms Evaluated

Platform Comparison:

```markdown
Platform Comparison:
├── Custom 3rd Party (LabelBox, Figure8)
│   └── ❌ Designed for images/text, not audio
├── LabelStudio (Open Source)
│   ├── ✅ Great UI, flexible, free
│   └── ❌ No RBAC, integration limitations
├── AWS GroundTruth + LabelStudio
│   ├── ✅ Full management features
│   └── ❌ Complex setup, poor UX, expensive ($9k/month)
└── Retool ✅ (Final Choice)
    ├── ✅ Quick setup (few days)
    ├── ✅ Custom dashboards
    ├── ✅ Progress tracking
    └── ✅ Cost-effective
```

### Retool Benefits for Audio Annotation:

- Built annotation interface in days, not weeks
- Custom progress tracking for annotators
- Manager dashboards for quality review
- Easy integration with existing backend

## Data Pipeline Architecture

### Data Processing Flow

```markdown
Annotation → Database → JSON Lines Manifest → Training
     ↓              ↓              ↓              ↓
  Retool UI    Filtered Data   W&B Artifacts   Model Training
```
### File Format Recommendations

- **JSON Lines (.jsonl)** for training manifests
- Each line: `{"audio_path": "...", "transcription": "...", "metadata": {...}}`
- Upload manifests to Weights & Biases for model provenance tracking

## Audio Processing Pipeline

### Minimal Processing Approach

- Handle audio standardization during **data collection**, not annotation
- If post-processing needed, use parallel processing:

```bash
# Tarteel's approach - process files in parallel for speed
find ${input_dir} -type f -name "*.${extension}" -print0 | \
parallel --bar -0 ffmpeg -y -hide_banner -loglevel error \
-i {} -ar ${sampling_freq_hz} -ac ${num_channels} \
${output_dir}/"{.}.${new_extension}"
```

### Why Parallel Processing

- Avoid "Argument list too long" errors with large datasets
- Significantly faster than sequential processing
- Essential for datasets with thousands of audio files

## Data Hosting Strategy

### Recommended Architecture

- **Database:** Store annotations and metadata
- **S3/Cloud Storage:** Store audio files
- **Training:** Download data directly on training instances (don't move GBs between instances)

### Manifest Generation

```markdown
# Create training manifest via Django management script
# Filter annotated data → Format as JSON Lines → Upload to W&B
# Leave actual audio download for training time
```

## Key Lessons for Whisper Finetuning

1. **Invest in Annotation Quality Early** - It's cheaper than retraining models
2. **Use Specialized Annotators** - Generic crowdsourcing fails for speech tasks
3. **Build Flexible Tools** - Retool > Complex AWS setups for most use cases
4. **Plan for Scale** - Use parallel processing and cloud storage from day one
5. **Track Data Provenance** - Link datasets to models for reproducibility

## Cost Optimization Tips

- **Avoid AWS GroundTruth** unless you have enterprise budget
- **Use contractor managers** instead of building annotation teams yourself
- **Leverage open-source tools** like LabelStudio + Retool combo
- **Process audio in parallel** to save compute time and costs
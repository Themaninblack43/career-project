# Career Quest RPG - Game Design Document
## "Turn Your Career Into An Actual Game"

---

## 🎮 CORE CONCEPT

### The Problem We're Solving
- Career planning is overwhelming and abstract
- Money/job stuff doesn't compute naturally for you
- Need clear progression systems and feedback loops
- Traditional advice is boring and doesn't stick

### The Solution
- Literal RPG where playing the game = doing career tasks
- Every real action gives XP, gold, achievements
- Clear quests with specific objectives
- Visual progress that mirrors real progress
- Save files to track everything

---

## 🏗️ ARCHITECTURE OVERVIEW

### Phase 1: Core Game Loop (What We Build First)
```
1. Character Creation (Your actual profile)
   ↓
2. Class Selection (Choose career path)
   ↓
3. Quest System (Real tasks as quests)
   ↓
4. Progress Tracking (XP, levels, achievements)
   ↓
5. Reward System (Unlock new content/paths)
```

### Technical Stack (Keep It Simple)
- **Frontend**: HTML5 + JavaScript (runs locally)
- **Storage**: LocalStorage for save games
- **Optional Later**: Node.js for advanced features
- **No servers needed**: Everything runs in browser

---

## 📋 FEATURE BREAKDOWN

### 1. CHARACTER SYSTEM

#### Your Character Stats (Based on Real Skills)
```javascript
character = {
    name: "Jeff",
    class: "Physics Graduate",
    level: 1,
    xp: 0,
    
    // Core Stats (from your cognitive profile)
    stats: {
        analysis: 90,      // Your constraint thinking
        technical: 85,     // Physics + problem solving
        systems: 95,       // Pattern recognition
        social: 40,        // Can level this up!
        business: 20,      // Starts low, will grow
        creativity: 75     // Cross-domain synthesis
    },
    
    // Resources
    resources: {
        energy: 100,       // Daily energy (ADHD management)
        focus: 100,        // Focus tokens for deep work
        gold: 0,           // Actual money earned
        reputation: 0      // Network/credibility
    }
}
```

#### Leveling System
- **XP Sources**: Complete real tasks
- **Level Benefits**: Unlock new quest types, higher pay quests
- **Skill Points**: Distribute to stats on level up

### 2. QUEST SYSTEM

#### Quest Types (Real Actions)
```javascript
quests = {
    daily: [
        {
            name: "Morning Routine",
            xp: 10,
            tasks: ["Make coffee", "Check calendar", "Set 3 priorities"],
            reward: "+20 energy for the day"
        },
        {
            name: "Apply to One Job",
            xp: 50,
            tasks: ["Find posting", "Customize resume", "Send application"],
            reward: "Roll for interview chance"
        }
    ],
    
    weekly: [
        {
            name: "Network Expansion",
            xp: 100,
            tasks: ["Join 1 new community", "Make 5 helpful comments", "DM 2 people"],
            reward: "+10 reputation"
        }
    ],
    
    epic: [
        {
            name: "First Client Project",
            xp: 500,
            tasks: ["Find client", "Deliver work", "Get testimonial"],
            reward: "Unlock Consultant Class"
        }
    ]
}
```

#### Quest UI Design
- Main quest line = Primary career path
- Side quests = Skill building
- Daily quests = Habit building
- Random encounters = Unexpected opportunities

### 3. CLASS/JOB SYSTEM

#### Starting Classes (Entry Level)
Each class has:
- Skill requirements
- Quest chains
- Evolution paths
- Special abilities

```javascript
classes = {
    dataAnalyst: {
        name: "Data Analyst",
        requirements: { analysis: 70, technical: 60 },
        startingQuests: ["Learn SQL", "Join Kaggle", "First Dataset"],
        evolution: "Data Scientist",
        specialAbility: "Pattern Recognition - 2x XP from data tasks"
    },
    // ... other classes
}
```

#### Class Evolution Tree
```
Data Analyst (Lvl 1-10)
    ↓
Data Scientist (Lvl 11-20)
    ↓
[Branch Choice]
ML Engineer / Analytics Manager
```

### 4. INVENTORY & SKILLS

#### Inventory System (Real Assets)
```javascript
inventory = {
    certificates: [],     // Actual certs earned
    portfolio: [],        // Completed projects
    tools: [],           // Software/skills learned
    connections: [],     // Network contacts
    documents: {
        resume: { level: 1, lastUpdated: "" },
        linkedIn: { complete: false },
        website: { url: "" }
    }
}
```

#### Skill Tree Example
```
Technical Tree:
├── SQL (Basic)
│   ├── SQL (Advanced)
│   │   └── Database Design
│   └── Data Visualization
│       ├── Tableau
│       └── PowerBI
```

### 5. ACHIEVEMENT SYSTEM

#### Achievement Categories
```javascript
achievements = {
    milestone: [
        { name: "First Application", icon: "📮", xp: 100 },
        { name: "10 Applications", icon: "📯", xp: 500 },
        { name: "First Interview", icon: "🎭", xp: 1000 }
    ],
    
    learning: [
        { name: "SQL Master", icon: "🗄️", xp: 300 },
        { name: "Certified", icon: "🏆", xp: 500 }
    ],
    
    legendary: [
        { name: "First Dollar Earned", icon: "💰", xp: 2000 },
        { name: "Full Time Job", icon: "👑", xp: 5000 }
    ]
}
```

### 6. GAME ECONOMY

#### Currency System
- **XP**: For leveling and unlocks
- **Gold**: Actual money tracking
- **Energy**: Daily action points (ADHD helper)
- **Focus Tokens**: For deep work sessions
- **Reputation**: Network strength

#### Energy Management (ADHD Feature)
```javascript
energySystem = {
    maxEnergy: 100,
    costs: {
        application: 30,
        networking: 20,
        learning: 25,
        deepWork: 50
    },
    restoration: {
        sleep: 100,
        break: 20,
        exercise: 30,
        hyperfocus: -50  // Penalty for overwork
    }
}
```

---

## 🎨 VISUAL DESIGN

### UI Layout
```
┌─────────────────────────────────────┐
│  [Avatar] Jeff - Lvl 3 Data Analyst │
│  HP: ████████░░  XP: 234/500        │
├─────────────────────────────────────┤
│  MAIN QUEST                         │
│  > Learn SQL Basics                 │
│    □ Complete Tutorial (0/5)        │
│    □ Join SQL Community            │
│                                     │
│  DAILY QUESTS           [Energy:70] │
│  ✓ Morning Routine      [+10 XP]    │
│  □ Apply to 1 Job       [-30 E]     │
│  □ Practice SQL         [-20 E]     │
├─────────────────────────────────────┤
│  [Inventory] [Skills] [Stats] [Map] │
└─────────────────────────────────────┘
```

### Visual Style Guide
- **16-bit pixel art** aesthetic
- **Color coding**: 
  - Green = Completed/Good
  - Yellow = In Progress/Warning
  - Red = Failed/Urgent
  - Blue = Information
  - Gold = Rewards/Achievements
- **Animations**: 
  - XP bar fills
  - Level up fanfare
  - Quest complete sparkles

---

## 🚀 IMPLEMENTATION PHASES

### Phase 1: MVP (Week 1-2)
Build basic working version:
1. Character creation/stats
2. Simple quest system
3. XP and leveling
4. Local storage save
5. Basic daily quests

### Phase 2: Quest Expansion (Week 3-4)
Add depth:
1. Full quest chains
2. Class selection
3. Skill trees
4. Achievement system
5. Energy management

### Phase 3: Visual Polish (Week 5-6)
Make it beautiful:
1. Sprite system
2. Animations
3. Sound effects
4. Particle effects
5. Better UI/UX

### Phase 4: Advanced Features (Week 7-8)
Add complexity:
1. Inventory system
2. NPC system (mentors/contacts)
3. Random events
4. Multiplayer leaderboard (optional)
5. Export progress reports

---

## 🎯 GAME MECHANICS THAT TEACH REAL SKILLS

### Mechanic → Real World Mapping

| Game Mechanic | Real World Skill |
|---------------|------------------|
| Energy management | ADHD daily planning |
| Quest priorities | Task prioritization |
| Skill points | Learning investment |
| Gold tracking | Financial awareness |
| Reputation system | Network building |
| Save scumming prevention | Commitment to choices |
| Cooldown timers | Sustainable pacing |
| Combo bonuses | Habit streaking |

### Progression Hooks (Keep You Playing/Working)

1. **Daily Login Bonus**: Compounds like real habits
2. **Streak System**: Don't break the chain
3. **Level Gates**: Must reach Level X to unlock certain jobs
4. **Rare Drops**: Random good opportunities from grinding
5. **Prestige System**: After getting job, can restart with bonuses

---

## 💾 SAVE SYSTEM

### What Gets Saved
```javascript
saveGame = {
    character: {...},
    completedQuests: [],
    currentQuests: [],
    inventory: {...},
    achievements: [],
    statistics: {
        totalApplications: 0,
        totalXP: 0,
        daysPlayed: 0,
        longestStreak: 0
    },
    realWorldProgress: {
        actualApplicationsSent: [],
        certificationsEarned: [],
        projectsCompleted: [],
        moneyEarned: 0
    }
}
```

### Auto-save Triggers
- Every quest completion
- Every level up
- Every 5 minutes
- On browser close

---

## 🔊 AUDIO DESIGN (Optional but Fun)

### Sound Effects Needed
- Level up fanfare
- Quest complete chime
- XP gain sound
- Achievement unlock
- Low energy warning
- Daily reset sound

### Music
- Calm exploration theme (job browsing)
- Battle music (interview prep)
- Victory theme (job offer)
- Town theme (main menu)

---

## 📊 METRICS & FEEDBACK LOOPS

### What We Track
- Daily active time
- Quest completion rate
- Real applications sent
- Skills learned
- Money earned/saved

### Weekly Report Card
```
WEEK 3 SUMMARY
--------------
Level: 2 → 3 [LEVEL UP!]
Quests: 12/15 completed
Applications: 5 sent
Interviews: 1 scheduled
Skills: +SQL, +Excel
Gold: +$500 (freelance)
Streak: 7 days

NEXT WEEK GOALS:
- Reach Level 4
- Complete SQL certification
- Send 10 applications
```

---

## 🎮 EXAMPLE DAY IN THE GAME

```
[MORNING]
> Daily Reset! Energy restored to 100
> Daily Quests Available:
  - Morning Routine [10 XP]
  - Apply to 1 Job [50 XP]
  - Learn for 30min [25 XP]

[PLAYER COMPLETES MORNING ROUTINE]
> +10 XP! 
> +20 Bonus Energy!
> Streak: 8 days

[PLAYER APPLIES TO DATA ANALYST JOB]
> -30 Energy
> +50 XP!
> Achievement: "5 Applications" unlocked!
> Random Drop: "Interview Scheduling Email"!

[AFTERNOON]
> Energy Low (40/100)
> Take break to restore? Y/N

[EVENING]
> Daily Summary:
  - XP Gained: 85
  - Progress to Level 4: 320/500
  - Tomorrow's bonus quest unlocked!
```

---

## 🚦 NEXT STEPS

### Immediate Actions
1. Build Phase 1 MVP
2. Test core loop for 1 week
3. Iterate based on what works
4. Add features gradually

### Success Metrics
- You actually use it daily
- Real applications increase
- Anxiety about career decreases
- Progress becomes visible
- Money starts coming in

---

## 💡 SPECIAL FEATURES FOR YOUR BRAIN

### ADHD Accommodations
- Visual progress everywhere
- Short, clear quests
- Energy system prevents burnout
- Lots of small wins
- Can pause/save anytime

### Asperger's Accommodations
- Clear, explicit rules
- No hidden information
- Predictable outcomes
- Systems-based logic
- Pattern recognition rewards

### Money Tracking Made Simple
- Gold = Real money
- Costs shown upfront
- ROI calculator built in
- Visual budget bars
- Automatic saving goals

---

*"This isn't just a game about getting a job. It's a systematic approach to life that happens to look like Final Fantasy."*
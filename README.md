# 🐍 Snake Game - Enchanted Garden

[Game Banner] (image-5.png)

A modern take on the classic Snake game featuring magical themes, progressive difficulty, golden food bonuses, dynamic obstacles, and smooth gameplay mechanics.

## 🌟 Overview

**Snake Game - Enchanted Garden** is a web-based arcade game where players control a magical snake exploring an enchanted garden to collect mystical fruits. The game features progressive difficulty, special golden fruits, dynamic obstacles, and an engaging scoring system.

### 🎯 Game Narrative
*You are a mystical snake exploring the Enchanted Garden, collecting magical fruits that grant you power and length. As you grow stronger, the garden reveals more challenges and rarer fruits. How long can you survive in this magical realm?*

---

## ✨ Features

### Core Gameplay
- 🐍 **Smooth snake movement** with responsive arrow key controls
- 🎮 **Classic mechanics** with modern enhancements
- 🧱 **Dynamic obstacles** that appear at higher levels
- 💥 **Particle effects** when collecting food
- 🔊 **Dynamic sound effects** for all game events
- 📊 **Grid-based movement** for precise control

### Scoring & Progression
- 🍎 **Regular Food** - 10 points (red apples)
- ⭐ **Golden Food** - 50 points (rare star fruits)
- 📈 **Progressive speed** - Increases every 5 foods
- 🏆 **High score tracking** with persistent storage
- 📊 **Level system** - Advance every 10 foods

### Difficulty Scaling
- ⚡ **Speed increases** gradually as you eat
- 🧱 **Obstacles spawn** starting at Level 3
- ⭐ **Golden food** appears more frequently at higher levels
- 📏 **Snake grows** with each food eaten
- 🎚️ **Dynamic difficulty** that adapts to your progress

### User Interface
- 🎨 **Modern green gradient** design matching garden theme
- 📊 **Real-time HUD** displaying Length, Score, Level, and Food Count
- ⏸️ **Pause functionality** (Press P or ESC)
- 📖 **Comprehensive instructions menu**
- 🏠 **Polished start/game over screens**
- 🌟 **Speed indicator** showing current game pace

---

## 🚀 How to Play

### Installation & Setup

1. **Clone the repository:**
```bash
git clone https://github.com/engracheal/Snake-game 
cd snake-game
```

2. **Open the game:**
   - Simply open `index.html` in any modern web browser
   - No installation or dependencies required!

3. **Play online:**
   - Visit: [https://github.com/engracheal/Snake-game]

### Controls

| Key | Action |
|-----|--------|
| `↑` Arrow Up | Move snake up |
| `↓` Arrow Down | Move snake down |
| `←` Arrow Left | Move snake left |
| `→` Arrow Right | Move snake right |
| `P` or `ESC` | Pause/Resume game |
| `🔊` Button | Toggle sound on/off |

### Game Rules

1. **Objective:** Collect as many fruits as possible to grow longer and score points
2. **Growth:** Your snake grows by 1 segment with each food eaten
3. **Losing:** Game ends if you hit:
   - Walls (screen boundaries)
   - Your own body
   - Obstacles (appear from Level 3)
4. **Winning:** Survive as long as possible and beat your high score

### Scoring System

| Item | Points | Spawn Rate |
|------|--------|------------|
| 🍎 Regular Food | 10 points | Common |
| ⭐ Golden Food | 50 points | Rare (10% + level bonus) |

**Progression Milestones:**
- Every 5 foods → Speed increases
- Every 10 foods → Level up + new obstacles (from Level 3)

---

## 🏗️ Technical Architecture

### Technology Stack
- **HTML5 Canvas** - For rendering game graphics
- **Vanilla JavaScript** - Game logic and mechanics
- **Web Audio API** - Dynamic sound generation
- **CSS3** - Modern UI styling with animations


### Class Architecture

The game follows **Object-Oriented Programming** principles:

#### Core Classes

**`Game`** - Main game controller
- Manages game state (menu, playing, paused, gameover)
- Handles game loop timing (speed-based updates)
- Coordinates all game objects
- Manages scoring and progression

**`Snake`** - Player-controlled snake
- Segment-based body structure
- Direction control with 180° turn prevention
- Growth mechanism
- Collision detection (self, walls, obstacles)
- Visual head distinction with eyes

**`Food`** - Collectible items
- Two types: Regular and Golden
- Smart spawning (avoids snake and obstacles)
- Visual distinction (circle vs star)
- Collision detection with snake head

**`Obstacle`** - Environmental hazards
- Grid-based positioning
- Level-dependent spawning
- Static barriers
- Collision detection

**`Particle`** - Visual effects system
- Explosion effects when food is collected
- Physics-based movement
- Life cycle management
- Color-matched to food type

**`SoundManager`** - Audio system
- Web Audio API integration
- Event-specific sounds (eat, golden, level up, game over)
- Mute/unmute functionality

---

## 🎮 Game Mechanics

### Snake Movement

**Grid-Based System:**
```javascript
- Snake moves one grid cell at a time
- Movement is direction-based (UP, DOWN, LEFT, RIGHT)
- Cannot reverse 180 degrees (prevents instant death)
- Head leads, body follows in segments
```

**Update Mechanism:**
```javascript
1. New head position calculated based on direction
2. New head added to front of segments array
3. Tail segment removed (unless growing)
4. Growing flag determines if tail stays
```

### Collision Detection

**Self-Collision:**
```javascript
checkSelfCollision() {
    const head = segments[0];
    return segments.slice(1).some(segment => 
        segment.x === head.x && segment.y === head.y
    );
}
```

**Wall Collision:**
```javascript
checkWallCollision() {
    return head.x < 0 || 
           head.x >= gridCols || 
           head.y < 0 || 
           head.y >= gridRows;
}
```

**Obstacle Collision:**
```javascript
checkObstacleCollision(obstacles) {
    return obstacles.some(obs => 
        obs.x === head.x && obs.y === head.y
    );
}
```

### Food System

**Regular Food:**
- Red apple appearance
- 10 points per collection
- Common spawn rate

**Golden Food:**
- Star-shaped appearance with glow
- 50 points per collection
- Base 10% spawn chance + level multiplier
- More frequent at higher levels

**Smart Spawning:**
```javascript
- Avoids all snake segments
- Avoids all obstacles
- Random position within grid bounds
- Respawns after collection
```

### Difficulty Progression

| Foods Eaten | Event | Effect |
|-------------|-------|--------|
| 5, 10, 15... | Speed Increase | Game tick rate decreases by 10ms |
| 10, 20, 30... | Level Up | Level counter increments |
| Level 3+ | Obstacles Spawn | Dynamic barriers appear |

**Speed Progression:**
```javascript
Initial: 150ms per move
Every 5 foods: -10ms
Minimum: 50ms (maximum difficulty)
```

**Obstacle Generation:**
```javascript
Count = min(floor(level / 2), 10)
- Level 3: 1-2 obstacles
- Level 5: 2-3 obstacles
- Level 10+: 5+ obstacles
- Maximum: 10 obstacles
```


### Main Menu
[Main Menu] (image.png)
*Enchanted Garden themed start screen*

### Gameplay
[Active Gameplay] (image-1.png)
*Snake navigating the grid with HUD display*

### Golden Food
[Golden Food Collection] (image-2.png)
*Rare golden star fruit with particle effects*

### Obstacles
[Obstacles Gameplay] (image-3.png)
*Higher level with multiple obstacles*

### Game Over
[Game Over Screen] (image-4.png)
*Final statistics and score display*

---

## 🧪 Testing & Quality Assurance

### Tested Scenarios

✅ **Movement Testing:**
- Arrow key responsiveness
- 180-degree turn prevention
- Smooth grid-based movement
- Direction queuing

✅ **Collision Testing:**
- Wall boundary detection
- Self-collision accuracy
- Obstacle collision
- Food collection detection

✅ **Progression Testing:**
- Speed increase timing
- Level advancement
- Obstacle spawning
- Golden food spawn rates

✅ **UI/UX Testing:**
- Menu navigation
- Pause/resume functionality
- HUD real-time updates
- Sound toggle

✅ **Edge Cases:**
- Rapid direction changes
- Food spawning on snake/obstacles
- Maximum snake length handling
- High score persistence

### Browser Compatibility

| Browser | Version | Status |
|---------|---------|--------|
| Chrome | 90+ | ✅ Fully Supported |
| Firefox | 88+ | ✅ Fully Supported |
| Safari | 14+ | ✅ Fully Supported |
| Edge | 90+ | ✅ Fully Supported |

---

## 🚧 Known Limitations & Future Enhancements

### Current Limitations
- Single-player only
- Fixed grid size (30×30)
- No save/load game state
- Web Audio API requires user interaction

### Planned Features
- 🎨 **Themed Levels** - Different garden environments
- 🏅 **Achievements System** - Unlock rewards for milestones
- 🎵 **Background Music** - Ambient garden soundscape
- 📱 **Mobile Support** - Touch/swipe controls
- 🎮 **Multiple Modes** - Classic, Time Attack, Survival
- 🌍 **More Power-ups** - Speed boost, invincibility, score multiplier
- 💾 **Save System** - Continue games across sessions
- 🎯 **Challenge Mode** - Specific goals and constraints
- 👥 **Multiplayer** - Compete or cooperate with friends


## 📚 Resources & Documentation

### Project Links
- 🎥 [Video Demo]
- 🌐 [Play Online](https://github.com/engracheal/Snake-game)
- 💻 [Source Code] (https://github.com/engracheal/Snake-game)

### Development Resources
- [HTML5 Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
- [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [JavaScript Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

---

## 📝 License

This project was created as coursework for educational purposes.

**Academic Use Only** - Not licensed for commercial distribution.

---


## 📞 Contact & Support

For questions or feedback about this project:

- **GitHub Issues:** [Create an issue](https://github.com/engracheal/Snake-game)
- **Email:** (ampumuzarecheal152@gmail.com)

---

## 🎉 Enjoy the Game!

*Explore the enchanted garden, collect magical fruits, and grow as long as you can!*

**Last Updated:** December 2025  
**Version:** 1.0.0

---

### Quick Start Commands

```bash
# Clone the repository
git clone https://github.com/engracheal/Snake-game 

# Navigate to directory
cd snake-game

# Open in browser (Mac)
open index.html

# Open in browser (Windows)
start index.html

# Open in browser (Linux)
xdg-open index.html
```

---

### Performance Tips

**For Best Experience:**
- Use a modern browser (Chrome/Firefox recommended)
- Close unnecessary tabs to maintain 60 FPS
- Enable sound for full immersion
- Use a keyboard with responsive arrow keys

---

### Gameplay Tips

**Beginner Tips:**
- 🎯 Plan your path ahead
- 🔄 Use the edges strategically
- ⭐ Golden food is worth the risk
- 🧘 Stay calm as speed increases

**Advanced Strategies:**
- 🌀 Create spiral patterns for safety
- 🎪 Use obstacles as reference points
- ⚡ Anticipate speed changes at 5-food intervals
- 🏆 Aim for golden food at higher levels for score boosts

**Record Attempts:**
- 📹 Record your high score runs
- 📊 Track your progress over time
- 🎯 Set personal goals (length, score, levels)
- 🤝 Challenge friends to beat your score

---

# Beat Buddy Java

🥁 Recreating Beat Buddy in a general way to learn JavaFX

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Development Guide](#development-guide)
- [JavaFX GUI Implementation](#javafx-gui-implementation)
- [Audio System](#audio-system)
- [Pattern Management](#pattern-management)
- [Building and Running](#building-and-running)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Drum Pattern Sequencer**: Create complex drum patterns with multiple tracks
- **Real-time Playback**: Low-latency audio playback engine
- **Custom JavaFX GUI**: Modern, responsive user interface
- **Pattern Library**: Save, load, and organize drum patterns
- **Tempo Control**: Adjustable BPM with tap tempo functionality
- **Multiple Drum Kits**: Switchable drum kit samples
- **Effects Processing**: Basic reverb and compression effects
- **MIDI Support**: Import/export MIDI files
- **Pattern Chaining**: Link patterns for song creation

## Prerequisites

- **Java Development Kit (JDK) 11+** with JavaFX included, OR
- **OpenJDK 11+** with **JavaFX SDK** downloaded separately
- **Audio samples** (WAV format recommended)

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/beatbuddy-clone.git
   cd beatbuddy-clone
   ```

2. **Download JavaFX (if not included with your JDK):**
   - Download JavaFX SDK from [openjfx.io](https://openjfx.io)
   - Extract to a directory (e.g., `/path/to/javafx-sdk-17`)

3. **Compile and run the application:**
   ```bash
   # If JavaFX is included in your JDK
   javac -d out src/main/java/com/beatbuddy/*.java src/main/java/com/beatbuddy/*/*.java
   java -cp out com.beatbuddy.BeatBuddyApp
   
   # If using separate JavaFX SDK
   javac --module-path /path/to/javafx-sdk-17/lib --add-modules javafx.controls,javafx.fxml,javafx.media -d out src/main/java/com/beatbuddy/*.java src/main/java/com/beatbuddy/*/*.java
   java --module-path /path/to/javafx-sdk-17/lib --add-modules javafx.controls,javafx.fxml,javafx.media -cp out com.beatbuddy.BeatBuddyApp
   ```

## Project Structure

```
beatbuddy-clone/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── beatbuddy/
│       │           ├── BeatBuddyApp.java              # Main application entry point
│       │           ├── controller/
│       │           │   ├── MainController.java        # Primary GUI controller
│       │           │   ├── PatternController.java     # Pattern editing logic
│       │           │   ├── PlaybackController.java    # Playback controls
│       │           │   └── SettingsController.java    # Application settings
│       │           ├── model/
│       │           │   ├── DrumKit.java              # Drum kit representation
│       │           │   ├── DrumPattern.java          # Pattern data structure
│       │           │   ├── DrumTrack.java            # Individual track data
│       │           │   ├── Step.java                 # Single step in pattern
│       │           │   └── AudioSample.java          # Audio sample wrapper
│       │           ├── audio/
│       │           │   ├── AudioEngine.java          # Core audio processing
│       │           │   ├── SamplePlayer.java         # Audio sample playback
│       │           │   ├── Sequencer.java            # Pattern sequencing
│       │           │   ├── EffectsProcessor.java     # Audio effects
│       │           │   └── MidiHandler.java          # MIDI import/export
│       │           ├── gui/
│       │           │   ├── components/
│       │           │   │   ├── StepButton.java       # Individual step buttons
│       │           │   │   ├── TrackStrip.java       # Track control strip
│       │           │   │   ├── PatternGrid.java      # Main pattern grid
│       │           │   │   ├── TransportControls.java # Play/stop/record buttons
│       │           │   │   └── VolumeSlider.java     # Custom volume control
│       │           │   ├── dialogs/
│       │           │   │   ├── SettingsDialog.java   # Settings configuration
│       │           │   │   ├── LoadPatternDialog.java # Pattern loading
│       │           │   │   └── SavePatternDialog.java # Pattern saving
│       │           │   └── utils/
│       │           │       ├── GuiUtils.java         # GUI utility methods
│       │           │       └── ThemeManager.java     # UI theming
│       │           ├── io/
│       │           │   ├── PatternFileManager.java   # Pattern file I/O
│       │           │   ├── AudioFileLoader.java     # Audio sample loading
│       │           │   └── ConfigurationManager.java # App configuration
│       │           └── utils/
│       │               ├── AudioUtils.java          # Audio utility functions
│       │               ├── Constants.java           # Application constants
│       │               └── Logger.java             # Custom logging
│       └── resources/
│           ├── fxml/
│           │   ├── main.fxml                        # Main window layout
│           │   ├── pattern-editor.fxml              # Pattern editor layout
│           │   └── settings.fxml                    # Settings dialog layout
│           ├── css/
│           │   ├── main.css                         # Main stylesheet
│           │   ├── dark-theme.css                   # Dark theme
│           │   └── light-theme.css                  # Light theme
│           ├── images/
│           │   ├── icons/                           # UI icons
│           │   └── backgrounds/                     # Background images
│           ├── audio/
│           │   ├── drum-kits/
│           │   │   ├── acoustic/                    # Acoustic drum samples
│           │   │   ├── electronic/                  # Electronic drum samples
│           │   │   └── vintage/                     # Vintage drum samples
│           │   └── samples/                         # Individual samples
│           └── patterns/
│               ├── rock/                            # Rock pattern presets
│               ├── jazz/                            # Jazz pattern presets
│               └── electronic/                      # Electronic pattern presets
├── lib/                                             # External JAR dependencies
│   ├── javafx-controls-17.jar                      # (if not using module path)
│   ├── javafx-fxml-17.jar                          # (if not using module path)
│   └── javafx-media-17.jar                         # (if not using module path)
├── out/                                             # Compiled .class files
├── scripts/
│   ├── compile.sh                                   # Compilation script (Unix/Mac)
│   ├── compile.bat                                  # Compilation script (Windows)
│   ├── run.sh                                       # Run script (Unix/Mac)
│   └── run.bat                                      # Run script (Windows)
├── docs/
│   ├── API.md                                       # API documentation
│   ├── DEVELOPMENT.md                               # Development guidelines
│   └── USER_GUIDE.md                               # User manual
├── test/
│   └── java/
│       └── com/
│           └── beatbuddy/
│               ├── audio/
│               │   ├── AudioEngineTest.java         # Audio engine tests
│               │   └── SequencerTest.java           # Sequencer tests
│               ├── model/
│               │   ├── DrumPatternTest.java         # Pattern model tests
│               │   └── DrumKitTest.java             # Drum kit tests
│               └── io/
│                   └── PatternFileManagerTest.java  # File I/O tests
├── README.md                                        # This file
└── LICENSE                                          # License file
```

## Getting Started

### 1. Understanding Beat Buddy Concepts

Beat Buddy is a drum machine that works with:
- **Patterns**: Sequences of drum hits arranged in steps
- **Tracks**: Individual drum sounds (kick, snare, hi-hat, etc.)
- **Steps**: Individual time divisions in a pattern (usually 16 steps)
- **Kits**: Collections of drum samples

### 2. Basic Architecture

The application follows the MVC (Model-View-Controller) pattern:
- **Model**: Data structures for patterns, tracks, and audio samples
- **View**: JavaFX-based GUI components
- **Controller**: Logic for handling user interactions and audio processing

### 3. Running Your First Pattern

1. Launch the application
2. Select a drum kit from the dropdown
3. Click on step buttons to create a pattern
4. Press play to hear your pattern
5. Adjust tempo and volume as needed

## Development Guide

### Core Components

#### 1. AudioEngine.java
The heart of the audio system, responsible for:
- Audio device initialization
- Sample playback timing
- Effects processing
- Real-time audio mixing

```java
package com.beatbuddy.audio;

import javax.sound.sampled.*;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class AudioEngine {
    private SourceDataLine audioLine;
    private AudioFormat audioFormat;
    private boolean isPlaying = false;
    private ExecutorService audioThreadPool;
    
    public AudioEngine() {
        audioThreadPool = Executors.newFixedThreadPool(4);
        initializeAudioSystem();
    }
    
    private void initializeAudioSystem() {
        try {
            audioFormat = new AudioFormat(44100, 16, 2, true, false);
            DataLine.Info info = new DataLine.Info(SourceDataLine.class, audioFormat);
            audioLine = (SourceDataLine) AudioSystem.getLine(info);
            audioLine.open(audioFormat, 4096);
            audioLine.start();
        } catch (LineUnavailableException e) {
            System.err.println("Audio initialization failed: " + e.getMessage());
        }
    }
    
    public void playSample(AudioSample sample, float volume) {
        if (audioLine != null && audioLine.isOpen()) {
            audioThreadPool.submit(() -> {
                byte[] audioData = sample.getProcessedAudioData(volume);
                audioLine.write(audioData, 0, audioData.length);
            });
        }
    }
    
    public void shutdown() {
        if (audioLine != null) {
            audioLine.drain();
            audioLine.close();
        }
        audioThreadPool.shutdown();
    }
}
```

#### 2. DrumPattern.java
Data structure for storing pattern information:

```java
package com.beatbuddy.model;

import java.io.Serializable;
import java.util.ArrayList;
import java.util.List;

public class DrumPattern implements Serializable {
    private String name;
    private int numSteps;
    private int bpm;
    private List<DrumTrack> tracks;
    
    public DrumPattern(String name, int numSteps, int bpm) {
        this.name = name;
        this.numSteps = numSteps;
        this.bpm = bpm;
        this.tracks = new ArrayList<>();
        initializeTracks();
    }
    
    private void initializeTracks() {
        String[] trackNames = {"Kick", "Snare", "Hi-Hat", "Open Hat", 
                              "Crash", "Ride", "Tom 1", "Tom 2"};
        for (String trackName : trackNames) {
            tracks.add(new DrumTrack(trackName, numSteps));
        }
    }
    
    public DrumTrack getTrack(int index) {
        return tracks.get(index);
    }
    
    public void setStep(int track, int step, boolean active) {
        tracks.get(track).setStep(step, active);
    }
    
    public boolean isStepActive(int track, int step) {
        return tracks.get(track).isStepActive(step);
    }
    
    // Getters and setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getNumSteps() { return numSteps; }
    public int getBpm() { return bpm; }
    public void setBpm(int bpm) { this.bpm = bpm; }
    public List<DrumTrack> getTracks() { return tracks; }
}
```

#### 3. Sequencer.java
Handles pattern playback timing:

```java
package com.beatbuddy.audio;

import com.beatbuddy.model.DrumPattern;
import com.beatbuddy.model.DrumKit;
import java.util.Timer;
import java.util.TimerTask;

public class Sequencer {
    private Timer timer;
    private DrumPattern currentPattern;
    private DrumKit currentKit;
    private AudioEngine audioEngine;
    private int currentStep = 0;
    private boolean isPlaying = false;
    private int bpm = 120;
    
    public Sequencer(AudioEngine audioEngine) {
        this.audioEngine = audioEngine;
    }
    
    public void play(DrumPattern pattern, DrumKit kit) {
        if (isPlaying) stop();
        
        this.currentPattern = pattern;
        this.currentKit = kit;
        this.bpm = pattern.getBpm();
        this.isPlaying = true;
        this.currentStep = 0;
        
        long stepDuration = (60000 / bpm) / 4; // 16th notes
        
        timer = new Timer();
        timer.scheduleAtFixedRate(new TimerTask() {
            @Override
            public void run() {
                playStep();
            }
        }, 0, stepDuration);
    }
    
    private void playStep() {
        for (int track = 0; track < currentPattern.getTracks().size(); track++) {
            if (currentPattern.isStepActive(track, currentStep)) {
                AudioSample sample = currentKit.getSample(track);
                if (sample != null) {
                    float volume = currentPattern.getTrack(track).getVolume();
                    audioEngine.playSample(sample, volume);
                }
            }
        }
        
        currentStep = (currentStep + 1) % currentPattern.getNumSteps();
    }
    
    public void stop() {
        if (timer != null) {
            timer.cancel();
            timer = null;
        }
        isPlaying = false;
        currentStep = 0;
    }
    
    public boolean isPlaying() { return isPlaying; }
    public int getCurrentStep() { return currentStep; }
    public void setBpm(int bpm) { this.bpm = bpm; }
}
```

## JavaFX GUI Implementation

### Main Application Class

```java
package com.beatbuddy;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;
import com.beatbuddy.controller.MainController;

public class BeatBuddyApp extends Application {
    
    @Override
    public void start(Stage primaryStage) {
        try {
            // Load FXML or create GUI programmatically
            BorderPane root = createMainLayout();
            Scene scene = new Scene(root, 1000, 700);
            
            // Load CSS
            scene.getStylesheets().add(
                getClass().getResource("/css/main.css").toExternalForm()
            );
            
            primaryStage.setTitle("Beat Buddy Clone");
            primaryStage.setScene(scene);
            primaryStage.show();
            
            // Handle application shutdown
            primaryStage.setOnCloseRequest(e -> {
                MainController.getInstance().shutdown();
            });
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    private BorderPane createMainLayout() {
        MainController controller = new MainController();
        return controller.createMainLayout();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

### Custom Components

#### StepButton.java
Custom JavaFX button for pattern steps:

```java
package com.beatbuddy.gui.components;

import javafx.scene.control.Button;
import javafx.scene.input.MouseButton;

public class StepButton extends Button {
    private boolean active = false;
    private int stepIndex;
    private int trackIndex;
    private StepButtonListener listener;
    
    public interface StepButtonListener {
        void onStepToggled(int track, int step, boolean active);
    }
    
    public StepButton(int step, int track) {
        this.stepIndex = step;
        this.trackIndex = track;
        setupButton();
    }
    
    private void setupButton() {
        setPrefSize(40, 40);
        getStyleClass().add("step-button");
        
        setOnMouseClicked(e -> {
            if (e.getButton() == MouseButton.PRIMARY) {
                toggleStep();
            } else if (e.getButton() == MouseButton.SECONDARY) {
                // Right-click for additional options
                showContextMenu();
            }
        });
        
        updateAppearance();
    }
    
    public void toggleStep() {
        active = !active;
        updateAppearance();
        if (listener != null) {
            listener.onStepToggled(trackIndex, stepIndex, active);
        }
    }
    
    private void updateAppearance() {
        if (active) {
            getStyleClass().removeAll("step-button");
            getStyleClass().add("step-button-active");
        } else {
            getStyleClass().removeAll("step-button-active");
            getStyleClass().add("step-button");
        }
    }
    
    private void showContextMenu() {
        // Implement context menu for velocity, etc.
    }
    
    public void setActive(boolean active) {
        this.active = active;
        updateAppearance();
    }
    
    public boolean isActive() { return active; }
    public void setListener(StepButtonListener listener) { this.listener = listener; }
}
```

#### PatternGrid.java
Central component displaying the step sequencer:

```java
package com.beatbuddy.gui.components;

import javafx.scene.layout.GridPane;
import javafx.scene.control.Label;
import javafx.geometry.Insets;

public class PatternGrid extends GridPane implements StepButton.StepButtonListener {
    private StepButton[][] stepButtons;
    private int numTracks = 8;
    private int numSteps = 16;
    private PatternGridListener listener;
    
    public interface PatternGridListener {
        void onStepChanged(int track, int step, boolean active);
    }
    
    public PatternGrid() {
        initializeGrid();
        setupStyling();
    }
    
    private void initializeGrid() {
        stepButtons = new StepButton[numTracks][numSteps];
        
        // Add track labels
        String[] trackNames = {"Kick", "Snare", "Hi-Hat", "Open Hat", 
                              "Crash", "Ride", "Tom 1", "Tom 2"};
        
        for (int track = 0; track < numTracks; track++) {
            Label trackLabel = new Label(trackNames[track]);
            trackLabel.getStyleClass().add("track-label");
            add(trackLabel, 0, track + 1);
            
            for (int step = 0; step < numSteps; step++) {
                StepButton button = new StepButton(step, track);
                button.setListener(this);
                stepButtons[track][step] = button;
                add(button, step + 1, track + 1);
            }
        }
        
        // Add step numbers
        for (int step = 0; step < numSteps; step++) {
            Label stepLabel = new Label(String.valueOf(step + 1));
            stepLabel.getStyleClass().add("step-label");
            add(stepLabel, step + 1, 0);
        }
    }
    
    private void setupStyling() {
        setHgap(2);
        setVgap(2);
        setPadding(new Insets(10));
        getStyleClass().add("pattern-grid");
    }
    
    @Override
    public void onStepToggled(int track, int step, boolean active) {
        if (listener != null) {
            listener.onStepChanged(track, step, active);
        }
    }
    
    public void setStepActive(int track, int step, boolean active) {
        stepButtons[track][step].setActive(active);
    }
    
    public void highlightCurrentStep(int step) {
        // Remove previous highlights
        for (int s = 0; s < numSteps; s++) {
            for (int t = 0; t < numTracks; t++) {
                stepButtons[t][s].getStyleClass().remove("current-step");
            }
        }
        
        // Add current step highlight
        if (step >= 0 && step < numSteps) {
            for (int t = 0; t < numTracks; t++) {
                stepButtons[t][step].getStyleClass().add("current-step");
            }
        }
    }
    
    public void clearPattern() {
        for (int track = 0; track < numTracks; track++) {
            for (int step = 0; step < numSteps; step++) {
                stepButtons[track][step].setActive(false);
            }
        }
    }
    
    public void setListener(PatternGridListener listener) {
        this.listener = listener;
    }
}
```

### Styling with CSS

Create modern, responsive UI with custom CSS in `src/main/resources/css/main.css`:

```css
/* Main application styling */
.root {
    -fx-background-color: #1e1e1e;
    -fx-font-family: "Arial";
}

/* Step buttons */
.step-button {
    -fx-min-width: 40px;
    -fx-min-height: 40px;
    -fx-max-width: 40px;
    -fx-max-height: 40px;
    -fx-background-color: #2c2c2c;
    -fx-border-color: #555555;
    -fx-border-width: 1px;
    -fx-background-radius: 4px;
    -fx-border-radius: 4px;
}

.step-button:hover {
    -fx-background-color: #3c3c3c;
    -fx-border-color: #777777;
}

.step-button-active {
    -fx-min-width: 40px;
    -fx-min-height: 40px;
    -fx-max-width: 40px;
    -fx-max-height: 40px;
    -fx-background-color: #ff6b35;
    -fx-border-color: #ff8c66;
    -fx-border-width: 2px;
    -fx-background-radius: 4px;
    -fx-border-radius: 4px;
}

.step-button-active:hover {
    -fx-background-color: #ff7a4a;
}

.current-step {
    -fx-effect: dropshadow(three-pass-box, #ffff00, 8, 0.3, 0, 0);
}

/* Transport controls */
.transport-button {
    -fx-min-width: 60px;
    -fx-min-height: 40px;
    -fx-font-size: 14px;
    -fx-font-weight: bold;
    -fx-background-color: #4a4a4a;
    -fx-text-fill: white;
    -fx-background-radius: 6px;
}

.transport-button:hover {
    -fx-background-color: #5a5a5a;
}

.play-button {
    -fx-background-color: #2e7d32;
}

.play-button:hover {
    -fx-background-color: #388e3c;
}

.stop-button {
    -fx-background-color: #d32f2f;
}

.stop-button:hover {
    -fx-background-color: #f44336;
}

/* Labels */
.track-label {
    -fx-text-fill: #cccccc;
    -fx-font-weight: bold;
    -fx-min-width: 80px;
    -fx-alignment: center-right;
    -fx-padding: 0 10 0 0;
}

.step-label {
    -fx-text-fill: #999999;
    -fx-font-size: 12px;
    -fx-alignment: center;
    -fx-min-width: 40px;
}

/* Pattern grid */
.pattern-grid {
    -fx-background-color: #252525;
    -fx-background-radius: 8px;
    -fx-effect: dropshadow(three-pass-box, rgba(0,0,0,0.3), 10, 0, 0, 2);
}

/* Volume sliders */
.volume-slider .thumb {
    -fx-background-color: #ff6b35;
}

.volume-slider .track {
    -fx-background-color: #444444;
}
```

## Audio System

### Sample Loading and Management

```java
package com.beatbuddy.io;

import com.beatbuddy.model.AudioSample;
import javax.sound.sampled.*;
import java.io.File;
import java.io.IOException;

public class AudioFileLoader {
    
    public static AudioSample loadSample(String filePath) {
        try {
            File audioFile = new File(filePath);
            AudioInputStream audioStream = AudioSystem.getAudioInputStream(audioFile);
            
            // Convert to standard format if necessary
            AudioFormat targetFormat = new AudioFormat(44100, 16, 2, true, false);
            if (!audioStream.getFormat().matches(targetFormat)) {
                audioStream = AudioSystem.getAudioInputStream(targetFormat, audioStream);
            }
            
            return new AudioSample(audioStream);
            
        } catch (UnsupportedAudioFileException | IOException e) {
            System.err.println("Failed to load audio sample: " + filePath);
            e.printStackTrace();
            return null;
        }
    }
    
    public static boolean isValidAudioFile(String filePath) {
        try {
            File audioFile = new File(filePath);
            AudioSystem.getAudioInputStream(audioFile);
            return true;
        } catch (Exception e) {
            return false;
        }
    }
}
```

### AudioSample Class

```java
package com.beatbuddy.model;

import javax.sound.sampled.AudioInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;

public class AudioSample {
    private byte[] audioData;
    private String name;
    private float defaultVolume = 1.0f;
    
    public AudioSample(AudioInputStream audioStream) {
        loadAudioData(audioStream);
    }
    
    private void loadAudioData(AudioInputStream audioStream) {
        try {
            ByteArrayOutputStream buffer = new ByteArrayOutputStream();
            byte[] tempBuffer = new byte[4096];
            int bytesRead;
            
            while ((bytesRead = audioStream.read(tempBuffer)) != -1) {
                buffer.write(tempBuffer, 0, bytesRead);
            }
            
            audioData = buffer.toByteArray();
            audioStream.close();
            
        } catch (IOException e) {
            System.err.println("Failed to load audio data: " + e.getMessage());
            audioData = new byte[0];
        }
    }
    
    public byte[] getProcessedAudioData(float volume) {
        if (audioData == null || audioData.length == 0) {
            return new byte[0];
        }
        
        byte[] processedData = new byte[audioData.length];
        
        // Apply volume (simple amplitude scaling)
        for (int i = 0; i < audioData.length; i += 2) {
            // Convert bytes to 16-bit sample
            short sample = (short) ((audioData[i + 1] << 8) | (audioData[i] & 0xFF));
            
            // Apply volume
            sample = (short) (sample * volume);
            
            // Convert back to bytes
            processedData[i] = (byte) (sample & 0xFF);
            processedData[i + 1] = (byte) ((sample >> 8) & 0xFF);
        }
        
        return processedData;
    }
    
    public byte[] getAudioData() { return audioData; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public float getDefaultVolume() { return defaultVolume; }
    public void setDefaultVolume(float volume) { this.defaultVolume = volume; }
}
```

## Building and Running

### Compilation Scripts

Create `scripts/compile.sh` (Unix/Mac):
```bash
#!/bin/bash

# Set JavaFX path (adjust as needed)
JAVAFX_PATH="/path/to/javafx-sdk-17/lib"

# Create output directory
mkdir -p out

# Compile all Java files
find src/main/java -name "*.java" > sources.txt

javac --module-path "$JAVAFX_PATH" \
      --add-modules javafx.controls,javafx.fxml,javafx.media \
      -cp src/main/resources \
      -d out \
      @sources.txt

# Copy resources
cp -r src/main/resources/* out/

# Clean up
rm sources.txt

echo "Compilation complete!"
```

Create `scripts/compile.bat` (Windows):
```batch
@echo off

REM Set JavaFX path (adjust as needed)
set JAVAFX_PATH=C:\path\to\javafx-sdk-17\lib

REM Create output directory
if not exist out mkdir out

REM Find all Java files
dir /s /B src\main\java\*.java > sources.txt

REM Compile
javac --module-path "%JAVAFX_PATH%" --add-modules javafx.controls,javafx.fxml,javafx.media -cp src\main\resources -d out @sources.txt

REM Copy resources
xcopy src\main\resources out\ /E /I /Y

REM Clean up
del sources.txt

echo Compilation complete!
```

### Run Scripts

Create `scripts/run.sh` (Unix/Mac):
```bash
#!/bin/bash

# Set JavaFX path
JAVAFX_PATH="/path/to/javafx-sdk-17/lib"

# Run the application
java --module-path "$JAVAFX_PATH" \
     --add-modules javafx.controls,javafx.fxml,javafx.media \
     -cp out \
     com.beatbuddy.BeatBuddyApp
```

Create `scripts/run.bat` (Windows):
```batch
@echo off

REM Set JavaFX path
set JAVAFX_PATH=C:\path\to\javafx-sdk-17\lib

REM Run the application
java --module-path "%JAVAFX_PATH%" --add-modules javafx.controls,javafx.fxml,javafx.media -cp out com.beatbuddy.BeatBuddyApp
```

### Manual Compilation and Running

#### Step 1: Compile the Project
```bash
# Create output directory
mkdir -p out

# Compile (with JavaFX module path)
javac --module-path /path/to/javafx-sdk-17/lib \
      --add-modules javafx.controls,javafx.fxml,javafx.media \
      -cp src/main/resources \
      -d out \
      src/main/java/com/beatbuddy/*.java \
      src/main/java/com/beatbuddy/*/*.java

# Copy resources
cp -r src/main/resources/* out/
```

#### Step 2: Run the Application
```bash
java --module-path /path/to/javafx-sdk-17/lib \
     --add-modules javafx.controls,javafx.fxml,javafx.media \
     -cp out \
     com.beatbuddy.BeatBuddyApp
```

#### Alternative: Using Classpath (if JavaFX JARs are in lib/)
```bash
# Compile
javac -cp "lib/*:src/main/resources" -d out src/main/java/com/beatbuddy/*.java src/main/java/com/beatbuddy/*/*.java

# Run
java -cp "out:lib/*" com.beatbuddy.BeatBuddyApp
```

## Pattern Management

### Saving and Loading Patterns

```java
package com.beatbuddy.io;

import com.beatbuddy.model.DrumPattern;
import java.io.*;

public class PatternFileManager {
    private static final String PATTERN_EXTENSION = ".bbp"; // Beat Buddy Pattern
    
    public static void savePattern(DrumPattern pattern, String filePath) {
        if (!filePath.endsWith(PATTERN_EXTENSION)) {
            filePath += PATTERN_EXTENSION;
        }
        
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream(filePath))) {
            oos.writeObject(pattern);
            System.out.println("Pattern saved: " + filePath);
        } catch (IOException e) {
            System.err.println("Failed to save pattern: " + e.getMessage());
        }
    }
    
    public static DrumPattern loadPattern(String filePath) {
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream(filePath))) {
            DrumPattern pattern = (DrumPattern) ois.readObject();
            System.out.println("Pattern loaded: " + filePath);
            return pattern;
        } catch (IOException | ClassNotFoundException e) {
            System.err.println("Failed to load pattern: " + e.getMessage());
            return null;
        }
    }
    
    public static void exportToMidi(DrumPattern pattern, String filePath) {
        // TODO: Implement MIDI export functionality
        System.out.println("MIDI export not yet implemented");
    }
    
    public static DrumPattern importFromMidi(String filePath) {
        // TODO: Implement MIDI import functionality
        System.out.println("MIDI import not yet implemented");
        return null;
    }
}
```

### Configuration Management

```java
package com.beatbuddy.io;

import java.io.*;
import java.util.Properties;

public class ConfigurationManager {
    private static final String CONFIG_FILE = "beatbuddy.properties";
    private Properties config;
    
    public ConfigurationManager() {
        config = new Properties();
        loadConfiguration();
    }
    
    private void loadConfiguration() {
        try (InputStream input = new FileInputStream(CONFIG_FILE)) {
            config.load(input);
        } catch (IOException e) {
            // Create default configuration
            createDefaultConfiguration();
        }
    }
    
    private void createDefaultConfiguration() {
        config.setProperty("audio.sampleRate", "44100");
        config.setProperty("audio.bufferSize", "4096");
        config.setProperty("gui.theme", "dark");
        config.setProperty("pattern.defaultBPM", "120");
        config.setProperty("pattern.defaultSteps", "16");
        config.setProperty("audio.defaultVolume", "0.8");
        
        saveConfiguration();
    }
    
    public void saveConfiguration() {
        try (OutputStream output = new FileOutputStream(CONFIG_FILE)) {
            config.store(output, "Beat Buddy Configuration");
        } catch (IOException e) {
            System.err.println("Failed to save configuration: " + e.getMessage());
        }
    }
    
    public String getProperty(String key, String defaultValue) {
        return config.getProperty(key, defaultValue);
    }
    
    public int getIntProperty(String key, int defaultValue) {
        try {
            return Integer.parseInt(config.getProperty(key, String.valueOf(defaultValue)));
        } catch (NumberFormatException e) {
            return defaultValue;
        }
    }
    
    public float getFloatProperty(String key, float defaultValue) {
        try {
            return Float.parseFloat(config.getProperty(key, String.valueOf(defaultValue)));
        } catch (NumberFormatException e) {
            return defaultValue;
        }
    }
    
    public void setProperty(String key, String value) {
        config.setProperty(key, value);
    }
}
```

## Main Controller Implementation

```java
package com.beatbuddy.controller;

import com.beatbuddy.audio.*;
import com.beatbuddy.model.*;
import com.beatbuddy.gui.components.*;
import com.beatbuddy.io.*;
import javafx.scene.layout.*;
import javafx.scene.control.*;
import javafx.geometry.Insets;
import javafx.application.Platform;

public class MainController implements PatternGrid.PatternGridListener {
    private static MainController instance;
    
    private AudioEngine audioEngine;
    private Sequencer sequencer;
    private DrumPattern currentPattern;
    private DrumKit currentKit;
    private ConfigurationManager config;
    
    // GUI Components
    private PatternGrid patternGrid;
    private TransportControls transportControls;
    private Slider tempoSlider;
    private Label tempoLabel;
    private ComboBox<String> kitSelector;
    
    public MainController() {
        instance = this;
        initialize();
    }
    
    public static MainController getInstance() {
        return instance;
    }
    
    private void initialize() {
        config = new ConfigurationManager();
        audioEngine = new AudioEngine();
        sequencer = new Sequencer(audioEngine);
        
        // Create default pattern
        int defaultBPM = config.getIntProperty("pattern.defaultBPM", 120);
        int defaultSteps = config.getIntProperty("pattern.defaultSteps", 16);
        currentPattern = new DrumPattern("New Pattern", defaultSteps, defaultBPM);
        
        // Load default drum kit
        loadDefaultDrumKit();
        
        // Setup sequencer callback for step highlighting
        setupSequencerCallback();
    }
    
    private void loadDefaultDrumKit() {
        currentKit = new DrumKit("Default Kit");
        
        // Load drum samples (adjust paths as needed)
        String[] samplePaths = {
            "src/main/resources/audio/drum-kits/acoustic/kick.wav",
            "src/main/resources/audio/drum-kits/acoustic/snare.wav",
            "src/main/resources/audio/drum-kits/acoustic/hihat.wav",
            "src/main/resources/audio/drum-kits/acoustic/openhat.wav",
            "src/main/resources/audio/drum-kits/acoustic/crash.wav",
            "src/main/resources/audio/drum-kits/acoustic/ride.wav",
            "src/main/resources/audio/drum-kits/acoustic/tom1.wav",
            "src/main/resources/audio/drum-kits/acoustic/tom2.wav"
        };
        
        for (int i = 0; i < samplePaths.length; i++) {
            AudioSample sample = AudioFileLoader.loadSample(samplePaths[i]);
            if (sample != null) {
                currentKit.setSample(i, sample);
            }
        }
    }
    
    private void setupSequencerCallback() {
        // This would need to be implemented in the Sequencer class
        // to provide callbacks for step updates
    }
    
    public BorderPane createMainLayout() {
        BorderPane root = new BorderPane();
        
        // Create menu bar
        MenuBar menuBar = createMenuBar();
        
        // Create main content
        VBox centerContent = new VBox(10);
        centerContent.setPadding(new Insets(10));
        
        // Transport controls
        transportControls = new TransportControls();
        setupTransportControls();
        
        // Tempo control
        HBox tempoControls = createTempoControls();
        
        // Kit selector
        HBox kitControls = createKitControls();
        
        // Pattern grid
        patternGrid = new PatternGrid();
        patternGrid.setListener(this);
        
        // Add components to layout
        centerContent.getChildren().addAll(
            transportControls,
            tempoControls,
            kitControls,
            patternGrid
        );
        
        root.setTop(menuBar);
        root.setCenter(centerContent);
        
        return root;
    }
    
    private MenuBar createMenuBar() {
        MenuBar menuBar = new MenuBar();
        
        // File menu
        Menu fileMenu = new Menu("File");
        MenuItem newItem = new MenuItem("New Pattern");
        MenuItem openItem = new MenuItem("Open Pattern...");
        MenuItem saveItem = new MenuItem("Save Pattern...");
        MenuItem exitItem = new MenuItem("Exit");
        
        newItem.setOnAction(e -> newPattern());
        openItem.setOnAction(e -> openPattern());
        saveItem.setOnAction(e -> savePattern());
        exitItem.setOnAction(e -> Platform.exit());
        
        fileMenu.getItems().addAll(newItem, openItem, saveItem, 
                                  new SeparatorMenuItem(), exitItem);
        
        // Edit menu
        Menu editMenu = new Menu("Edit");
        MenuItem clearItem = new MenuItem("Clear Pattern");
        MenuItem settingsItem = new MenuItem("Settings...");
        
        clearItem.setOnAction(e -> clearPattern());
        settingsItem.setOnAction(e -> showSettings());
        
        editMenu.getItems().addAll(clearItem, new SeparatorMenuItem(), settingsItem);
        
        menuBar.getMenus().addAll(fileMenu, editMenu);
        return menuBar;
    }
    
    private void setupTransportControls() {
        transportControls.getPlayButton().setOnAction(e -> playPattern());
        transportControls.getStopButton().setOnAction(e -> stopPattern());
        transportControls.getRecordButton().setOnAction(e -> toggleRecord());
    }
    
    private HBox createTempoControls() {
        HBox tempoBox = new HBox(10);
        tempoBox.setAlignment(javafx.geometry.Pos.CENTER_LEFT);
        
        Label tempoLabelText = new Label("BPM:");
        tempoSlider = new Slider(60, 200, currentPattern.getBpm());
        tempoSlider.setShowTickLabels(true);
        tempoSlider.setShowTickMarks(true);
        tempoSlider.setMajorTickUnit(20);
        tempoSlider.setMinorTickCount(4);
        tempoSlider.setPrefWidth(200);
        
        tempoLabel = new Label(String.valueOf(currentPattern.getBpm()));
        tempoLabel.setMinWidth(40);
        
        tempoSlider.valueProperty().addListener((obs, oldVal, newVal) -> {
            int bpm = newVal.intValue();
            tempoLabel.setText(String.valueOf(bpm));
            currentPattern.setBpm(bpm);
            sequencer.setBpm(bpm);
        });
        
        Button tapTempoButton = new Button("Tap");
        tapTempoButton.setOnAction(e -> tapTempo());
        
        tempoBox.getChildren().addAll(tempoLabelText, tempoSlider, tempoLabel, tapTempoButton);
        return tempoBox;
    }
    
    private HBox createKitControls() {
        HBox kitBox = new HBox(10);
        kitBox.setAlignment(javafx.geometry.Pos.CENTER_LEFT);
        
        Label kitLabel = new Label("Drum Kit:");
        kitSelector = new ComboBox<>();
        kitSelector.getItems().addAll("Acoustic", "Electronic", "Vintage");
        kitSelector.setValue("Acoustic");
        kitSelector.setOnAction(e -> loadDrumKit(kitSelector.getValue()));
        
        kitBox.getChildren().addAll(kitLabel, kitSelector);
        return kitBox;
    }
    
    // Event handlers
    private void playPattern() {
        if (sequencer.isPlaying()) {
            sequencer.stop();
        } else {
            sequencer.play(currentPattern, currentKit);
        }
    }
    
    private void stopPattern() {
        sequencer.stop();
    }
    
    private void toggleRecord() {
        // TODO: Implement recording functionality
        System.out.println("Recording not yet implemented");
    }
    
    private void newPattern() {
        stopPattern();
        int bpm = config.getIntProperty("pattern.defaultBPM", 120);
        int steps = config.getIntProperty("pattern.defaultSteps", 16);
        currentPattern = new DrumPattern("New Pattern", steps, bpm);
        patternGrid.clearPattern();
        tempoSlider.setValue(bpm);
    }
    
    private void openPattern() {
        // TODO: Implement file chooser dialog
        System.out.println("Open pattern dialog not yet implemented");
    }
    
    private void savePattern() {
        // TODO: Implement file chooser dialog
        System.out.println("Save pattern dialog not yet implemented");
    }
    
    private void clearPattern() {
        stopPattern();
        patternGrid.clearPattern();
        for (int track = 0; track < currentPattern.getTracks().size(); track++) {
            for (int step = 0; step < currentPattern.getNumSteps(); step++) {
                currentPattern.setStep(track, step, false);
            }
        }
    }
    
    private void showSettings() {
        // TODO: Implement settings dialog
        System.out.println("Settings dialog not yet implemented");
    }
    
    private void tapTempo() {
        // TODO: Implement tap tempo functionality
        System.out.println("Tap tempo not yet implemented");
    }
    
    private void loadDrumKit(String kitName) {
        // TODO: Implement kit loading based on selection
        System.out.println("Loading kit: " + kitName);
    }
    
    @Override
    public void onStepChanged(int track, int step, boolean active) {
        currentPattern.setStep(track, step, active);
    }
    
    public void shutdown() {
        sequencer.stop();
        audioEngine.shutdown();
        config.saveConfiguration();
    }
}
```

## Testing

### Running Tests

```bash
# Compile tests
javac -cp out:lib/* -d out test/java/com/beatbuddy/*/*.java

# Run tests (example with simple test runner)
java -cp out:lib/* com.beatbuddy.audio.AudioEngineTest
```

### Simple Test Example

```java
package com.beatbuddy.model;

public class DrumPatternTest {
    public static void main(String[] args) {
        testPatternCreation();
        testStepManipulation();
        System.out.println("All tests passed!");
    }
    
    private static void testPatternCreation() {
        DrumPattern pattern = new DrumPattern("Test", 16, 120);
        assert pattern.getName().equals("Test");
        assert pattern.getNumSteps() == 16;
        assert pattern.getBpm() == 120;
        assert pattern.getTracks().size() == 8;
    }
    
    private static void testStepManipulation() {
        DrumPattern pattern = new DrumPattern("Test", 16, 120);
        
        // Test setting and getting steps
        pattern.setStep(0, 0, true);
        assert pattern.isStepActive(0, 0) == true;
        
        pattern.setStep(0, 0, false);
        assert pattern.isStepActive(0, 0) == false;
    }
}
```

## Deployment

### Creating a Runnable JAR

Create a simple script to package everything:

```bash
#!/bin/bash
# package.sh

# Create manifest file
cat > manifest.txt << EOF
Main-Class: com.beatbuddy.BeatBuddyApp
Class-Path: lib/javafx-controls-17.jar lib/javafx-fxml-17.jar lib/javafx-media-17.jar lib/javafx-base-17.jar lib/javafx-graphics-17.jar
EOF

# Create JAR
jar cfm BeatBuddy.jar manifest.txt -C out .

# Clean up
rm manifest.txt

echo "JAR created: BeatBuddy.jar"
echo "Run with: java -jar BeatBuddy.jar"
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Follow the existing code style and structure
4. Test your changes thoroughly
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Code Style Guidelines

- Use 4 spaces for indentation
- Follow Java naming conventions
- Add JavaDoc comments for public methods
- Keep methods focused and concise
- Use meaningful variable names
- Handle exceptions appropriately

## Troubleshooting

### Common Issues

1. **JavaFX Not Found**: Ensure JavaFX is properly installed and the module path is correct
2. **Audio Issues**: Check that your system supports the audio formats being used
3. **Missing Resources**: Verify that resource files are copied to the output directory
4. **Performance Issues**: Consider adjusting buffer sizes in the audio configuration

### Debug Mode

Add debug flags when running:
```bash
java -Djavafx.verbose=true -Djava.util.logging.level=INFO --module-path /path/to/javafx-sdk-17/lib --add-modules javafx.controls,javafx.fxml,javafx.media -cp out com.beatbuddy.BeatBuddyApp
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Inspired by the original Beat Buddy drum machine
- JavaFX community for excellent UI framework
- Java Sound API documentation and examples
- Contributors and testers

---

**Happy Drumming! 🥁**

*For questions or support, please open an issue on GitHub.*
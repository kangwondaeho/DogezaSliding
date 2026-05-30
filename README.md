# Dogeza Sliding - Simplified Core Build

Lecture06-Modulization 구조를 기반으로 만든 원버튼 타이밍 게임입니다.
기존 `GameLoop -> GameObject -> Component` 구조를 유지하고, 게임에 필요한 핵심 기능만 컴포넌트로 분리했습니다.

## Controls

- Space: title confirm / start approach / prone slide
- R: restart round
- ESC: quit

## Game Rule

플레이어는 리시버 앞에서 최대한 가깝게 멈춰야 합니다.

- `playerZ >= receiverZ`: FAIL
- `0 < receiverZ - playerZ <= 25`: PERFECT
- `25 < receiverZ - playerZ <= 60`: GREAT
- `60 < receiverZ - playerZ <= 120`: GOOD
- `120 < receiverZ - playerZ`: FAIL

## Score Rule

- PERFECT: +1000
- GREAT: +700
- GOOD: +300
- FAIL: current score reset to 0
- BEST score is preserved

## Core Components

- `MapRandomizerComponent`: selects one of three map rules
- `DepthTargetComponent`: stores receiver target Z position
- `ProneSlideComponent`: controls approach and prone slide movement
- `JudgeComponent`: calculates final distance and result
- `ScoreComponent`: manages current score, best score, and last score
- `GameStateMachineComponent`: controls TITLE / READY / APPROACH / PRONE_SLIDE / JUDGE / RESULT
- `FollowCameraComponent`: follows player depth position
- `BackgroundZoomComponent`: displays map background and projects world Z to screen
- `PlayerVisualComponent`: switches player run/prone texture
- `ReceiverVisualComponent`: places receiver on the background track
- `TitleOverlayComponent`: controls title image visibility
- `TitleBackdropComponent`: controls title backdrop
- `BitmapFontHudComponent`: renders score, map, and guide text
- `ResultImageOverlayComponent`: displays PERFECT / GREAT / GOOD / FAIL result texture

## Files

### Engine / Framework

- `Framework.hpp`
- `GraphicsContext.hpp`
- `WindowContext.hpp`
- `Timer.hpp`
- `ObjectBase.hpp`
- `GameLoop.hpp`
- `Material.hpp`
- `Mesh.hpp`
- `MeshRenderer.hpp`
- `Texture.hpp`

### Game

- `DogezaTypes.hpp`
- `DogezaComponents.hpp`
- `main.cpp`

### Shaders

- `effect.hlsl`
- `texture.hlsl`

### Assets

- `assets/bg_map_stop.png`
- `assets/bg_map_short.png`
- `assets/bg_map_long.png`
- `assets/player_run.png`
- `assets/player_prone.png`
- `assets/receiver.png`
- `assets/font_atlas.png`
- `assets/title_card.png`
- `assets/result_perfect.png`
- `assets/result_great.png`
- `assets/result_good.png`
- `assets/result_fail.png`

## Removed From Final Simplified Build

The following files/features were removed because they were not part of the core gameplay explanation:

- post-processing bloom shader files
- unused original background image file
- unused receiver halo image file
- proximity halo components
- result flash / halo burst / fail slash effects
- camera shake effect
- distance meter
- console debug HUD
- unused `PlayerControl.hpp` sample component

## Build

Open `DogezaSliding.sln` in Visual Studio 2022 and build Debug x64.
The project uses `/utf-8`.

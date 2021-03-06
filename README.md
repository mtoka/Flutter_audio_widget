# audio_widget

[![sample](./medias/sample.gif)](https://github.com/florent37/Flutter_audio_widget)

(this widget does not display anything)

Play an audio on flutter can be as simple as display an image ! Just add a widget into the tree

```dart
Audio.assets(
  path: "assets/audios/country.mp3",
  play: true, //AudioWidget does not maintain the play state
  child: ...
)
```

# ⏯ Play / Pause

Like usual Flutter widgets, just update the parameters of the `Audio`

```dart
//inside a stateful widget

bool _play = false;

@override
Widget build(BuildContext context) {
  return Audio.assets(
     path: "assets/audios/country.mp3",
     play: _play,
     child: RaisedButton(
       child: Text(
         _play ? "pause" : "play",
       ),
       onPressed: () {
         setState(() {
           _play = !_play;
         });
       },
     ),
  );
}
```

# 🛑 How to stop ?

Just remove the Audio from the tree !
Or simply keep `play: false`

# ⏩ How to seek ?

Just update the `initialPosition` of the Audio

```dart
//inside a stateful widget

Duration _seek;

@override
Widget build(BuildContext context) {
  return Audio.assets(
     path: "assets/audios/country.mp3",
     play: true,
     initialPosition: _seek,
     child: RaisedButton(
       child: Text("seek"),
       onPressed: () {
         setState(() {
           _seek = Duration(seconds: 30);
         });
       },
     ),
  );
}
```

# 🙉 Listeners

```dart
Audio.assets(
  path: "assets/audios/country.mp3",
  play: _play,

  onReadyToPlay: (duration) {
     //onReadyToPlay
  },
  
  onPositionChanged: (current, duration) {
     //onReadyToPlay
  },

  child: ...
)
```

# 💽 Player

By default, `Audio` uses [Assets Audio Player](https://pub.dev/packages/assets_audio_player) to play its songs

You can change it just by create a new wrapper of `AudioWidgetPlayer`

```dart
class AudioWidgetMyPlayer extends AudioWidgetPlayer {
  final MyPlayer _player = MyPlayer();

  @override
  void play() => _player.play();

  @override
  void pause() => _player.pause();

  //etc.
```

and update the `defaultAudioWidgetPlayer` inside your main

```
void main() {
    defaultAudioWidgetPlayer = () => AudioWidgetMyPlayer();
    runApp(MyApp());
}
```

import React, { useState, useEffect } from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import TrackPlayer, { State, usePlaybackState } from 'react-native-track-player';
import { Ionicons } from '@expo/vector-icons';

const RadioPlayer = () => {
  const playbackState = usePlaybackState();
  const [isPlaying, setIsPlaying] = useState(false);

  useEffect(() => {
    setupPlayer();
  }, []);

  const setupPlayer = async () => {
    await TrackPlayer.setupPlayer();
    await TrackPlayer.add({
      id: '1',
      url: 'https://tu-streaming-url.com/stream',
      title: 'Corvalen FM',
      artist: 'Radio Cristiana',
    });
  };

  const togglePlayback = async () => {
    if (playbackState === State.Playing) {
      await TrackPlayer.pause();
      setIsPlaying(false);
    } else {
      await TrackPlayer.play();
      setIsPlaying(true);
    }
  };

  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center', backgroundColor: '#eef' }}>
      <Text style={{ fontSize: 24, fontWeight: 'bold', marginBottom: 20 }}>Corvalen FM</Text>
      <TouchableOpacity onPress={togglePlayback} style={{ padding: 20, backgroundColor: '#333', borderRadius: 10 }}>
        <Ionicons name={isPlaying ? 'pause' : 'play'} size={30} color='white' />
      </TouchableOpacity>
    </View>
  );
};

export default RadioPlayer;

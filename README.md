# LuaJIT-SDL2
autogenerated LuaJIT bindings for SDL2 2.26.0

Set CMake LUAJIT_BIN to the LuaJIT directory for installing.

See test folder examples for usage

luajit-async (taken from https://github.com/sonoro1234/luajit-async) needs to be installed for providing lua functions that can be called from another thread (sdl.MakeAudioCallback and sdl.MakeThreadFunc).

This repo is used in https://github.com/sonoro1234/LuaJIT-ImGui where you get very usefull GUI widgets.

All above can be found at https://github.com/sonoro1234/anima

# sdlAudioPlayer

simple interface for playing sndfile files from disk

```lua
local sndf = require"LuaJIT-libsndfile"
local AudioPlayer = require"sdlAudioPlayer"

--copy specs from file
local info = sndf.get_info(filename)
local audioplayer,err = AudioPlayer({
    --device = device_name, --nil as device
    freq = info.samplerate, 
    format = sdl.AUDIO_S16SYS,
    channels = info.channels, 
    samples = 1024})

--insert several files
for i=1,10 do
	--filename, level, timeoffset
	audioplayer:insert(filename,(11-i)*0.1,i*0.6)
end
--show them
for node in audioplayer:nodes() do
    print("node",node.sf)
end

--play them 7 secs
audioplayer:start()
sdl.Delay(7000);
--close
audioplayer:close()
```

# Introduction
These detections are aimed at detecting poor efforts at patching ACEs within the exploit environment.

# ACE function error check
This detection aims to check the returned permission error of the target ACE function.

```lua
local ExpectedError = "The current thread cannot access 'MessageBusService' (lacking capability RobloxScript)"

local function AttemptACECall()
	game:GetService("MessageBusService"):Publish()
end

while true do
	local ErrorResult = select(2, pcall(AttemptACECall))

	if ErrorResult ~= ExpectedError then
		print("Poor ACE Patch detected!") -- or some form of punishment
	end

	task.wait(5)
end
```
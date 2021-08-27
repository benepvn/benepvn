--Make on trucmai

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local autorob = Instance.new("TextButton")

--Properties:

ScreenGui.Parent = game.CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(66, 255, 214)
Frame.Position = UDim2.new(0.241486073, 0, 0.432273269, 0)
Frame.Size = UDim2.new(0, 216, 0, 100)
Frame.Active = true	
Frame.Draggable = true

autorob.Name = "autorob"
autorob.Parent = Frame
autorob.BackgroundColor3 = Color3.fromRGB(144, 53, 255)
autorob.Position = UDim2.new(0, 0, 0.439999998, 0)
autorob.Size = UDim2.new(0, 200, 0, 50)
autorob.Font = Enum.Font.SourceSans
autorob.TextColor3 = Color3.fromRGB(0, 0, 0)
autorob.TextSize = 14.000
autorob.MouseButton1Down:connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/alohabeach/Main/master/Scripts/JailbreakAutoRob.lua"))()
end)


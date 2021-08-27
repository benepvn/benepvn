-- Make on XTrucMaiX2k3
local main = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local fly = Instance.new("TextButton")
local noclip = Instance.new("TextButton")
local ten = Instance.new("TextLabel")
local speed = Instance.new("TextButton")
local speedorigin = Instance.new("TextButton")

--Properties:

main.Name = "main"
main.Parent = game.CoreGui
main.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Frame.Parent = main
Frame.BackgroundColor3 = Color3.fromRGB(255, 152, 154)
Frame.Position = UDim2.new(0.106037155, 0, 0.468786806, 0)
Frame.Size = UDim2.new(0, 400, 0, 253)
Frame.Active = true
Frame.Draggable = true

fly.Name = "fly"
fly.Parent = Frame
fly.BackgroundColor3 = Color3.fromRGB(255, 190, 210)
fly.Position = UDim2.new(0.498335898, 0, 0.593639553, 0)
fly.Size = UDim2.new(0, 200, 0, 90)
fly.Font = Enum.Font.SourceSans
fly.Text = "fly"
fly.TextColor3 = Color3.fromRGB(255, 0, 255)
fly.TextSize = 25.000
fly.MouseButton1Down:connect(function()
	repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Head") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
	local mouse = game.Players.LocalPlayer:GetMouse() 
	repeat wait() until mouse
	local plr = game.Players.LocalPlayer 
	local torso = plr.Character.Head 
	local flying = false
	local deb = true 
	local ctrl = {f = 0, b = 0, l = 0, r = 0} 
	local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
	local maxspeed = 400 
	local speed = 5000 

	function Fly() 
		local bg = Instance.new("BodyGyro", torso) 
		bg.P = 9e4 
		bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
		bg.cframe = torso.CFrame 
		local bv = Instance.new("BodyVelocity", torso) 
		bv.velocity = Vector3.new(0,0.1,0) 
		bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
		repeat wait() 
			plr.Character.Humanoid.PlatformStand = true 
			if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
				speed = speed+.5+(speed/maxspeed) 
				if speed > maxspeed then 
					speed = maxspeed 
				end 
			elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
				speed = speed-1 
				if speed < 0 then 
					speed = 0 
				end 
			end 
			if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
				lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
			elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
			else 
				bv.velocity = Vector3.new(0,0.1,0) 
			end 
			bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
		until not flying 
		ctrl = {f = 0, b = 0, l = 0, r = 0} 
		lastctrl = {f = 0, b = 0, l = 0, r = 0} 
		speed = 0 
		bg:Destroy() 
		bv:Destroy() 
		plr.Character.Humanoid.PlatformStand = false 
	end 
	mouse.KeyDown:connect(function(key) 
		if key:lower() == "f" then 
			if flying then flying = false 
			else 
				flying = true 
				Fly() 
			end 
		elseif key:lower() == "w" then 
			ctrl.f = 1 
		elseif key:lower() == "s" then 
			ctrl.b = -1 
		elseif key:lower() == "a" then 
			ctrl.l = -1 
		elseif key:lower() == "d" then 
			ctrl.r = 1 
		end 
	end) 
	mouse.KeyUp:connect(function(key) 
		if key:lower() == "w" then 
			ctrl.f = 0 
		elseif key:lower() == "s" then 
			ctrl.b = 0 
		elseif key:lower() == "a" then 
			ctrl.l = 0 
		elseif key:lower() == "d" then 
			ctrl.r = 0 
		end 
	end)
	Fly()
end)

noclip.Name = "noclip"
noclip.Parent = Frame
noclip.BackgroundColor3 = Color3.fromRGB(255, 190, 210)
noclip.Position = UDim2.new(-0.00396284834, 0, 0.593639553, 0)
noclip.Size = UDim2.new(0, 200, 0, 90)
noclip.Font = Enum.Font.SourceSans
noclip.Text = "noclip 'c'"
noclip.TextColor3 = Color3.fromRGB(0, 0, 0)
noclip.TextSize = 30.000
noclip.MouseButton1Down:connect(function()
	noclip = false
	game:GetService('RunService').Stepped:connect(function()
		if noclip then
			game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
		end
	end)
	plr = game.Players.LocalPlayer
	mouse = plr:GetMouse()
	mouse.KeyDown:connect(function(key)

		if key == "c" then
			noclip = not noclip
			game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
		end
	end)
	print('Loaded')
	print('Press "c" to noclip')
end)

ten.Name = "ten"
ten.Parent = Frame
ten.BackgroundColor3 = Color3.fromRGB(255, 190, 210)
ten.Position = UDim2.new(0.248436525, 0, 0.00356149673, 0)
ten.Size = UDim2.new(0, 200, 0, 50)
ten.Font = Enum.Font.SourceSans
ten.Text = "Gui speed & Fly | Make XtrucMaiX2k3"
ten.TextColor3 = Color3.fromRGB(255, 0, 255)
ten.TextSize = 15.000

speed.Name = "speed"
speed.Parent = Frame
speed.BackgroundColor3 = Color3.fromRGB(255, 190, 210)
speed.Position = UDim2.new(0, 0, 0.260869563, 0)
speed.Size = UDim2.new(0, 200, 0, 75)
speed.Font = Enum.Font.SourceSans
speed.Text = "Speed 120"
speed.TextColor3 = Color3.fromRGB(0, 0, 0)
speed.TextSize = 38.000
speed.MouseButton1Down:connect(function()
	game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 120
end)

speedorigin.Name = "speed origin"
speedorigin.Parent = Frame
speedorigin.BackgroundColor3 = Color3.fromRGB(255, 190, 210)
speedorigin.Position = UDim2.new(0.5, 0, 0.260869563, 0)
speedorigin.Size = UDim2.new(0, 202, 0, 75)
speedorigin.Font = Enum.Font.SourceSans
speedorigin.Text = "speed origrin"
speedorigin.TextColor3 = Color3.fromRGB(0, 0, 0)
speedorigin.TextSize = 14.000
speedorigin.MouseButton1Down:connect(function()
	game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
end)

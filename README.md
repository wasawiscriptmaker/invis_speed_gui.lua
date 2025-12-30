-- GUI Invisible + Velocidad | Delta Mobile

local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local humanoid = char:WaitForChild("Humanoid")

player.CharacterAdded:Connect(function(c)
	char = c
	humanoid = char:WaitForChild("Humanoid")
end)

local gui = Instance.new("ScreenGui")
gui.Parent = player.PlayerGui
gui.ResetOnSpawn = false

local frame = Instance.new("Frame")
frame.Parent = gui
frame.Size = UDim2.new(0, 200, 0, 160)
frame.Position = UDim2.new(0.05, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true

local invisBtn = Instance.new("TextButton")
invisBtn.Parent = frame
invisBtn.Size = UDim2.new(0, 180, 0, 40)
invisBtn.Position = UDim2.new(0, 10, 0, 10)
invisBtn.Text = "Invisible"
invisBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
invisBtn.TextColor3 = Color3.new(1,1,1)

local invisible = false

invisBtn.MouseButton1Click:Connect(function()
	invisible = not invisible
	for _,v in pairs(char:GetDescendants()) do
		if v:IsA("BasePart") and v.Name ~= "HumanoidRootPart" then
			v.Transparency = invisible and 1 or 0
			if v:FindFirstChild("face") then
				v.face.Transparency = invisible and 1 or 0
			end
		end
	end
	invisBtn.Text = invisible and "Visible" or "Invisible"
end)

local speedBox = Instance.new("TextBox")
speedBox.Parent = frame
speedBox.Size = UDim2.new(0, 180, 0, 35)
speedBox.Position = UDim2.new(0, 10, 0, 65)
speedBox.PlaceholderText = "Velocidad (ej: 50)"
speedBox.BackgroundColor3 = Color3.fromRGB(60,60,60)
speedBox.TextColor3 = Color3.new(1,1,1)
speedBox.Text = ""

local speedBtn = Instance.new("TextButton")
speedBtn.Parent = frame
speedBtn.Size = UDim2.new(0, 180, 0, 35)
speedBtn.Position = UDim2.new(0, 10, 0, 110)
speedBtn.Text = "Aplicar Velocidad"
speedBtn.BackgroundColor3 = Color3.fromRGB(80,80,80)
speedBtn.TextColor3 = Color3.new(1,1,1)

speedBtn.MouseButton1Click:Connect(function()
	local spd = tonumber(speedBox.Text)
	if spd then
		humanoid.WalkSpeed = spd
	end
end)

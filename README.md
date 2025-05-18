-- NATAN DEAD REAILS | Delta & Android | Feito por ChatGPT

-- Proteção e UI base
pcall(function() game.CoreGui.NDR:Destroy() end)

local NDR = Instance.new("ScreenGui", game.CoreGui)
NDR.Name = "NDR"
NDR.ResetOnSpawn = false

local Frame = Instance.new("Frame", NDR)
Frame.Size = UDim2.new(0, 360, 0, 420)
Frame.Position = UDim2.new(0.5, -180, 0.5, -210)
Frame.BackgroundColor3 = Color3.new(0, 0, 0)
Frame.BorderSizePixel = 0
Frame.Active = true
Frame.Draggable = true

local UICorner = Instance.new("UICorner", Frame)
UICorner.CornerRadius = UDim.new(0, 10)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "NATAN DEAD REAILS"
Title.TextColor3 = Color3.new(1, 0, 0)
Title.Font = Enum.Font.GothamBlack
Title.TextScaled = true

-- Função de criar botões
local function createButton(name, callback)
	local btn = Instance.new("TextButton", Frame)
	btn.Size = UDim2.new(1, -20, 0, 35)
	btn.Position = UDim2.new(0, 10, 0, 40 + (#Frame:GetChildren()-2)*38)
	btn.BackgroundColor3 = Color3.new(0.15, 0.15, 0.15)
	btn.TextColor3 = Color3.new(1, 1, 1)
	btn.Font = Enum.Font.GothamBold
	btn.Text = name
	btn.TextScaled = true

	local corner = Instance.new("UICorner", btn)
	corner.CornerRadius = UDim.new(0, 8)

	btn.MouseButton1Click:Connect(callback)
end

-- Funções úteis e testadas:
createButton("TP para o Trem", function()
	for _,v in pairs(game:GetService("Workspace"):GetDescendants()) do
		if v.Name == "Train" and v:IsA("Model") then
			game.Players.LocalPlayer.Character:PivotTo(v:GetPivot())
		end
	end
end)

createButton("TP para a Base 1", function()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-263, 40, 440)
end)

createButton("TP para a Base 2", function()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(900, 38, -600)
end)

createButton("TP para Final da Linha", function()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5000, 100, 0)
end)

createButton("FullBright", function()
	game.Lighting.Brightness = 2
	game.Lighting.ClockTime = 12
	game.Lighting.FogEnd = 100000
end)

createButton("Remover Neblina", function()
	game.Lighting.FogEnd = 999999
end)

createButton("Unlock Mouse", function()
	game:GetService("UserInputService").MouseIconEnabled = true
end)

createButton("Unlock Camera", function()
	game:GetService("UserInputService").MouseBehavior = Enum.MouseBehavior.Default
end)

createButton("ESP Inimigos", function()
	for _,v in pairs(game.Players:GetPlayers()) do
		if v ~= game.Players.LocalPlayer then
			local highlight = Instance.new("Highlight", v.Character or v.CharacterAdded:Wait())
			highlight.FillColor = Color3.new(1, 0, 0)
			highlight.OutlineColor = Color3.new(1, 1, 1)
		end
	end
end)

createButton("Kill Aura", function()
	while task.wait(0.2) do
		pcall(function()
			for _,v in pairs(game.Players:GetPlayers()) do
				if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("Humanoid") then
					if (v.Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 15 then
						game.ReplicatedStorage:WaitForChild("Damage"):FireServer(v.Character.Humanoid, math.random(20,30))
					end
				end
			end
		end)
	end
end)

createButton("Ativar Noclip", function()
	local noclip = true
	game:GetService("RunService").Stepped:Connect(function()
		if noclip then
			for _,v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
				if v:IsA("BasePart") then
					v.CanCollide = false
				end
			end
		end
	end)
end)

-- Notificação final
game.StarterGui:SetCore("SendNotification", {
	Title = "NDR HUB",
	Text = "Script ativado com sucesso!",
	Duration = 5
})

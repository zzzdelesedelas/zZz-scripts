-- MeepCity Script Avançado - AutoFarm Peixe + Clonar Skin + Voar + Invisível
-- ⚠️ Compatível com JJSploit / executores simples

-- Criando a GUI
local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "VNSTOP7_HUB"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 320, 0, 320)
frame.Position = UDim2.new(0.35, 0, 0.35, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true
frame.ClipsDescendants = true
frame.BackgroundTransparency = 0.1
frame.AnchorPoint = Vector2.new(0.5, 0.5)

-- Cantos arredondados
local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0, 10)

-- Título
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "🐟 VNSTOP7 HUB"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextSize = 24

-- Nome do jogador (input)
local nameBox = Instance.new("TextBox", frame)
nameBox.PlaceholderText = "Nome do jogador"
nameBox.Size = UDim2.new(0, 260, 0, 30)
nameBox.Position = UDim2.new(0, 30, 0, 50)
nameBox.BackgroundColor3 = Color3.fromRGB(35,35,35)
nameBox.TextColor3 = Color3.fromRGB(255,255,255)
nameBox.Font = Enum.Font.Gotham
nameBox.TextSize = 16
nameBox.BorderSizePixel = 0
Instance.new("UICorner", nameBox).CornerRadius = UDim.new(0, 8)

-- Botão clonar skin
local cloneBtn = Instance.new("TextButton", frame)
cloneBtn.Text = "✨ Clonar Skin"
cloneBtn.Size = UDim2.new(0, 260, 0, 35)
cloneBtn.Position = UDim2.new(0, 30, 0, 90)
cloneBtn.BackgroundColor3 = Color3.fromRGB(70,130,180)
cloneBtn.TextColor3 = Color3.fromRGB(255,255,255)
cloneBtn.Font = Enum.Font.GothamBold
cloneBtn.TextSize = 18
cloneBtn.BorderSizePixel = 0
Instance.new("UICorner", cloneBtn).CornerRadius = UDim.new(0, 8)

-- Botão AutoFarm
local farmBtn = Instance.new("TextButton", frame)
farmBtn.Text = "🎣 Iniciar AutoFarm"
farmBtn.Size = UDim2.new(0, 260, 0, 35)
farmBtn.Position = UDim2.new(0, 30, 0, 135)
farmBtn.BackgroundColor3 = Color3.fromRGB(34,139,34)
farmBtn.TextColor3 = Color3.fromRGB(255,255,255)
farmBtn.Font = Enum.Font.GothamBold
farmBtn.TextSize = 18
farmBtn.BorderSizePixel = 0
Instance.new("UICorner", farmBtn).CornerRadius = UDim.new(0, 8)

-- Botões extras (Voar e Invisibilidade)
local flyBtn = Instance.new("TextButton", frame)
flyBtn.Text = "🕊️ Voar"
flyBtn.Size = UDim2.new(0, 260, 0, 35)
flyBtn.Position = UDim2.new(0, 30, 0, 180)
flyBtn.BackgroundColor3 = Color3.fromRGB(0,191,255)
flyBtn.TextColor3 = Color3.fromRGB(255,255,255)
flyBtn.Font = Enum.Font.GothamBold
flyBtn.TextSize = 18
flyBtn.BorderSizePixel = 0
Instance.new("UICorner", flyBtn).CornerRadius = UDim.new(0, 8)

local invisBtn = Instance.new("TextButton", frame)
invisBtn.Text = "👻 Invisível"
invisBtn.Size = UDim2.new(0, 260, 0, 35)
invisBtn.Position = UDim2.new(0, 30, 0, 225)
invisBtn.BackgroundColor3 = Color3.fromRGB(238,130,238)
invisBtn.TextColor3 = Color3.fromRGB(255,255,255)
invisBtn.Font = Enum.Font.GothamBold
invisBtn.TextSize = 18
invisBtn.BorderSizePixel = 0
Instance.new("UICorner", invisBtn).CornerRadius = UDim.new(0, 8)

-- Botão fechar
local closeBtn = Instance.new("TextButton", frame)
closeBtn.Text = "❌ Fechar"
closeBtn.Size = UDim2.new(0, 260, 0, 30)
closeBtn.Position = UDim2.new(0, 30, 0, 270)
closeBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 16
closeBtn.BorderSizePixel = 0
Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 8)

-- Função: Clonar Skin
cloneBtn.MouseButton1Click:Connect(function()
	local playerName = nameBox.Text
	local localPlayer = game.Players.LocalPlayer
	local targetPlayer = game.Players:FindFirstChild(playerName)
	if targetPlayer then
		-- Clona a skin do jogador selecionado
		localPlayer.CharacterAppearance = "https://www.roblox.com/avatar-thumbnail-3d/json?userId=" .. targetPlayer.UserId
		localPlayer:LoadCharacter()
		nameBox.Text = "Skin clonada com sucesso!"
	else
		nameBox.Text = "Jogador não encontrado"
	end
end)

-- Função: AutoFarm
local farming = false
farmBtn.MouseButton1Click:Connect(function()
	farming = not farming
	if farming then
		farmBtn.Text = "🎣 AutoFarm Ativo"
		farmBtn.BackgroundColor3 = Color3.fromRGB(60,180,75)
		spawn(function()
			while farming do
				wait(math.random(2, 5)) -- Intervalo variável para pesca
				local fishingRod = game:GetService("ReplicatedStorage"):FindFirstChild("FishingRodUsed")
				if fishingRod then
					fishingRod:FireServer() -- Dispara a pesca
				end
			end
		end)
	else
		farmBtn.Text = "🎣 Iniciar AutoFarm"
		farmBtn.BackgroundColor3 = Color3.fromRGB(34,139,34)
	end
end)

-- Função: Voar
local flying = false
flyBtn.MouseButton1Click:Connect(function()
	flying = not flying
	local character = game.Players.LocalPlayer.Character
	if flying then
		flyBtn.Text = "🕊️ Voar Ativo"
		local bodyVelocity = Instance.new("BodyVelocity")
		bodyVelocity.MaxForce = Vector3.new(10000, 10000, 10000)
		bodyVelocity.Velocity = Vector3.new(50, 50, 50)
		bodyVelocity.Parent = character:WaitForChild("HumanoidRootPart")
	else
		flyBtn.Text = "🕊️ Voar"
		for _, child in pairs(character:WaitForChild("HumanoidRootPart"):GetChildren()) do
			if child:IsA("BodyVelocity") then
				child:Destroy()
			end
		end
	end
end)

-- Função: Invisível
local invisible = false
invisBtn.MouseButton1Click:Connect(function()
	invisible = not invisible
	local character = game.Players.LocalPlayer.Character
	if invisible then
		invisBtn.Text = "👻 Invisível Ativo"
		character:WaitForChild("Head").Transparency = 0
		character:WaitForChild("Humanoid").Health = 0
	else
		invisBtn.Text = "👻 Invisível"
		character:WaitForChild("Head").Transparency = 0
		character:WaitForChild("Humanoid").Health = 100
	end
end)

-- Função: Fechar
closeBtn.MouseButton1Click:Connect(function()
	gui:Destroy()
end)

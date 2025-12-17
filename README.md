-- Este script deve ser colocado em StarterPlayer > StarterCharacterScripts

local Players = game:GetService("Players")

local function createAura(character)
    -- Verifica se a aura já existe para não duplicar
    if character:FindFirstChild("AuraParticles") then return end

    -- Cria uma nova partícula
    local aura = Instance.new("ParticleEmitter")
    aura.Name = "AuraParticles"
    aura.Texture = "rbxassetid://4848025235" -- Exemplo de textura circular/bonita
    aura.Color = ColorSequence.new(Color3.fromRGB(255, 182, 193)) -- Rosa Sakura
    aura.LightEmission = 0.8
    aura.Size = NumberSequence.new(2)
    aura.Rate = 30
    aura.Speed = NumberRange.new(0.5,1)
    aura.Lifetime = NumberRange.new(1,1.5)
    aura.Parent = character:FindFirstChild("HumanoidRootPart")
    -- Opção: adapte o Parent se quiser colocar em outro lugar do corpo
end

local function onCharacterAdded(character)
    -- Espera HumanoidRootPart existir
    local hrp = character:WaitForChild("HumanoidRootPart", 5)
    if not hrp then return end
    createAura(character)
end

local player = Players.LocalPlayer
if player.Character then
    onCharacterAdded(player.Character)
end
player.CharacterAdded:Connect(onCharacterAdded)

local fireDelay = 0.2 - Atraso entre disparos

local fireSound = "rbxassetid://207197037" - Som de disparo

local reloadTime = 2 -- Tempo de recarga

local ammo = 12 - Quantidade de munição inicial

local currentAmmo = ammo - Quantidade de munição atual

local isReloading = false - Estado de recarga

Função de recarga

local function reload()

if isReloading then return end

isReloading = true

currentAmmo = ammo

game.Workspace. Pistol: PlayAnimation("reload")

wait(reloadTime)

isReloading = false

end

Função de disparo

local function fire()

if not (currentAmmo > 0) then return end

currentAmmo = currentAmmo - 1

game.Workspace. Bullet: PlayAnimation("shoot")

game.Workspace. Pistol: PlayAnimation("fire")

wait(fireDelay)

local firePos = game. Workspace.Pistol.FirePos

local fireDir = game. Workspace. Pistol.FireDir

local bullet = Instance.new("Part")

bullet.Parent = game. Workspace

bullet. Anchored = true

bullet.Position = firePos

bullet.Size = Vector3.new(0.1, 0.1, 0.1)

bullet.Material = Enum.Material.Neon

bullet.Color = Color3.new(1, 0, 0)

bullet. Transparency = 0

bullet.CanCollide = false

bullet.Touched:Connect(function(hit)

if hit.Parent:FindFirstChild("Humanoid") then

local humanoid = hit.Parent:FindFirstChild("Humanoid")

humanoid: TakeDamage (10)

bullet:Destroy()

end

end)

game.Debris:AddItem(bullet, 2)

end

Evento de pressão da tecla Z

game:GetService("UserInputService").Input Began:Connect(function(input)

if input.KeyCode == Enum.KeyCode.Z then

if not isReloading then

fire()

else

reload()

end end

end)

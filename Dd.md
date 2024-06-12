
local Spawner = loadstring(game:HttpGet("https://raw.githubusercontent.com/huyhoangphuc/a120doors/main/jghgifgy"))()

---====== Create entity ======---

wait(2)
game.Lighting.MainColorCorrection.TintColor = Color3.fromRGB(255, 0, 0)
game.Lighting.MainColorCorrection.Contrast = 1
local tween = game:GetService("TweenService")
tween:Create(game.Lighting.MainColorCorrection, TweenInfo.new(2.5), {Contrast = 0}):Play()
local TweenService = game:GetService("TweenService")
local TW = TweenService:Create(game.Lighting.MainColorCorrection, TweenInfo.new(80),{TintColor = Color3.fromRGB(255, 255, 255)})
TW:Play()

local entity = Spawner.createEntity({
    CustomName = "Claim",
    Model = "rbxassetid:////11403215085", -- Your entity's model url here ("rbxassetid://1234567890" or GitHub raw url)
    Speed = 0,
    MoveDelay = 1,
    HeightOffset = 2,
    CanKill = false,
    KillRange = 5,
    SpawnInFront = true,
    ShatterLights = false,
    FlickerLights = {
        Enabled = false,
        Duration = 3
    },
    Cycles = {
        Min = 1,
        Max = 1,
        Delay = 0
    },
    CamShake = {
        Enabled = true,
        Values = {9.5, 20, 0.1, 1},
        Range = 5
    },
    ResistCrucifix = true,
    BreakCrucifix = true,
    DeathMessage = {"you die to A-10", "yee."},
    IsCuriousLight = true
})

---====== Debug ======---

entity.Debug.OnEntitySpawned = function()
     wait(5)
     game.Workspace:FindFirstChild("Claim"):Destroy()
end

entity.Debug.OnEntityDespawned = function()
    local achievementGiver = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors/Custom%20Achievements/Source.lua"))()

---====== Display achievement ======---
achievementGiver({
    Title = "",
    Desc = "You can die",
    Reason = "Claim Entity Hardcore",
    Image = "rbxassetid://11867753039"
})
end
entity.Debug.OnEntityStartMoving = function()
    print("1403134642614031346426")
end

entity.Debug.OnEntityFinishedRebound = function()
    print("Entity finished rebound")
end

entity.Debug.OnEntityEnteredRoom = function(room)
    if  game.ReplicatedStorage.GameData.LatestRoom.Value ~= 50 then
game.ReplicatedStorage.GameData.LatestRoom.Changed:Wait()
else
Wait(0)
end

game.Players.LocalPlayer.Character.Humanoid:TakeDamage(1000)
end

entity.Debug.OnLookAtEntity = function()
    game.Players.LocalPlayer.Character.Humanoid:TakeDamage(20)
end

entity.Debug.OnDeath = function()
    print("Player has died")
end

--[[
    NOTE: By overwriting 'OnUseCrucifix', the default crucifixion will be ignored and this function will be called instead

    entity.Debug.OnUseCrucifix = function()
        print("Custom crucifixion script here")
    end
]]--

---====== Run entity ======---

Spawner.runEntity(entity)

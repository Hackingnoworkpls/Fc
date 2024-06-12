function loopdamage()
while true do wait(1)
pcall(function()
end
game.Players.LocalPlayer.Character.Humanoid:TakeDamage(10)
end)
end
end





pcall(function()
local loopdamagePas = coroutine.wrap(loopdamage)
loopdamagePas()
end)

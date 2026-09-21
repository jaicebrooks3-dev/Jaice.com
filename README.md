# Jaice.com
local Players = game:GetService("Players")

local combo = {}
local lastAttack = {}

local MAX_COMBO = 4
local COMBO_RESET_TIME = 1

Players.PlayerAdded:Connect(function(player)
	combo[player] = 0
	lastAttack[player] = 0
end)

Players.PlayerRemoving:Connect(function(player)
	combo[player] = nil
	lastAttack[player] = nil
end)

local function attack(player)
	local now = os.clock()

	if now - lastAttack[player] > COMBO_RESET_TIME then
		combo[player] = 0
	end

	combo[player] += 1
	lastAttack[player] = now

	if combo[player] > MAX_COMBO then
		combo[player] = 1
	end

	print(player.Name .. " performed combo hit " .. combo[player])

	-- Damage, animations, and effects ca

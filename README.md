# esx_defib

Requirements

-esx  V1final or lower 
-esx_ambulancejob
-add defib's to your db

Open the defibrillator respitory attached to this, copy that code into your client side ambulance job 

HOW TO ADD DEFIB TO DB:
run this in your database sql query and adjust to your server limits 

INSERT INTO `items` (`id`, `name`, `label`, `limit`, `rare`, `can_remove`) VALUES (NULL, 'defib', 'Defibrillator', '-1', '0', '1');

HOW TO ADJUST AMBULANCE JOB SERVER.LUA
```
Open esx_ambulancejob>server>main/lua and find this
 
RegisterNetEvent('esx_ambulancejob:revive')
AddEventHandler('esx_ambulancejob:revive', function(playerId)
    local xPlayer = ESX.GetPlayerFromId(source)

    if xPlayer and xPlayer.job.name == 'ambulance' then
        local xTarget = ESX.GetPlayerFromId(playerId)

Replace the above line with the below line

RegisterServerEvent('esx_ambulancejob:revive')
AddEventHandler('esx_ambulancejob:revive', function(target)
    local xPlayer = ESX.GetPlayerFromId(source)

    xPlayer.addMoney(Config.ReviveReward)
    TriggerClientEvent('esx_ambulancejob:revive', target)
end)```

You are done, everyday citizens(non medics) can now use the defib and revive downed players

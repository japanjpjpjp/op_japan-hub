local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "japan hub",
   LoadingTitle = "japan hub Loading...",
   LoadingSubtitle = "by op_japan",
   ConfigurationSaving = { Enabled = false },
   KeySystem = false
})

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local Debris = game:GetService("Debris")
local LocalPlayer = Players.LocalPlayer
local HttpService = game:GetService("HttpService")

local GrabEvents = ReplicatedStorage:FindFirstChild("GrabEvents")
local CharacterEvents = ReplicatedStorage:FindFirstChild("CharacterEvents")
local MenuToys = ReplicatedStorage:FindFirstChild("MenuToys")

local SetNetworkOwner = GrabEvents and GrabEvents:FindFirstChild("SetNetworkOwner")
local CreateGrabLine = GrabEvents and GrabEvents:FindFirstChild("CreateGrabLine")
local DestroyGrabLine = GrabEvents and GrabEvents:FindFirstChild("DestroyGrabLine")
local RagdollRemote = CharacterEvents and CharacterEvents:FindFirstChild("RagdollRemote")
local Struggle = CharacterEvents and CharacterEvents:FindFirstChild("Struggle")
local SpawnToyRemoteFunction = MenuToys and MenuToys:FindFirstChild("SpawnToyRemoteFunction")
local DestroyToy = MenuToys and MenuToys:FindFirstChild("DestroyToy")

local function getMyRoot() local c = LocalPlayer.Character; return c and c:FindFirstChild("HumanoidRootPart") end
local function isFriend(player) local s, r = pcall(function() return LocalPlayer:IsFriendsWith(player.UserId) end); return s and r end
local function UpdatePlayerLists() local o = {}; for _, p in Players:GetPlayers() do if p ~= LocalPlayer then table.insert(o, p.DisplayName) end end; return o end

-- 冷笑スパム
local spamEnabled, targetPlayerName, targetDisplayName, spamTimer, lastMessage, currentIndex = false, "", "", 0, "", 1
local prefix = { "", "まじで", "ガチで", "ほんとに", "冗談抜きで", "普通に", "シンプルに", "あのさ、", "ねえ、", "ちょっと", "え、", "いや、", "だからさ、", "マジで", "ガチで", "超", "めっちゃ", "くそ" }
local targetWords = { "", "お前", "君", "あなた", "そこの", "この", "あの", "例の", "自称", "元", "えあぷ", "ざこ", "ていすぺ", "かきんへい", "はいじん", "自称ぷろ", "ねっとみん", "きっず", "みん", "さん" }
local insults = { "ｷﾁｨ～🤓😅", "お、おう😅", "お、おう🤓", "えぐすぎぃー🤓", "草🤓", "それな🤓😅", "え？🤓", "ウケる🤓", "マジかよ🤓", "知らんけど🤓😅", "はいはい🤓", "なるほどね🤓😅", "そういうことね🤓", "ちょっと何言ってるかわかんないっすね…🤓😅", "頭大丈夫？🤓", "病院行った方がいいよ🤓😅", "日本語理解できますか？🤓", "小学生からやり直した方がいいよ🤓😅", "思考停止してて草🤓", "その発言で自分のレベルバレてるよ🤓😅", "えあぷ乙🤓", "知識浅すぎて泣ける🤓😅", "恥ずかしくないの？🤓", "よくそんなんで生きてこれたね🤓😅", "親泣くぞ🤓", "ネットやめた方がいいよ🤓😅", "視野狭すぎて草🤓", "固定観念やばいね🤓😅", "それ本気で言ってる？🤓", "ネタだよね？🤓😅", "滑ってるよ🤓", "寒い寒い🥶🤓", "誰も笑ってないよ🤓😅", "ドンマイ🤓", "おつかれー🤓😅", "ご苦労様です🤓", "いんきゃっぽい発言🤓😅", "ようきゃのフリすんなよ🤓", "こみゅしょう乙🤓😅", "友達いないのバレちゃうよ🤓", "かまってちゃんなの？🤓😅", "寂しいんだね🤓", "構ってほしくて必死で草🤓😅", "チーッス🤓", "おっす🤓😅", "元気？🤓", "やきうのお兄ちゃんかな？🤓😅", "ネットべんけい乙🤓😅", "リアルでは震えてそう🤓", "声小さそう🤓😅", "顔真っ赤にしてそう🤓", "キーボード叩く手が震えてるよ🤓😅", "画面の前でぶちぎれてるの想像して草🤓", "悔しそうでワロタ🤓😅", "反論できないんだね🤓", "論破されて草🤓😅", "ぐうの音も出ない正論🤓", "黙っちゃった🤓😅", "逃げるんだね🤓" }
local allMessages = {}
for _, p in ipairs(prefix) do for _, t in ipairs(targetWords) do for _, i in ipairs(insults) do local msg = p .. t .. i; if #msg < 60 then table.insert(allMessages, msg) end end end end
for i = #allMessages, 2, -1 do local j = math.random(i); allMessages[i], allMessages[j] = allMessages[j], allMessages[i] end

local function sendChat(text) pcall(function() if game:GetService("TextChatService").ChatVersion == Enum.ChatVersion.TextChatService then local c = game:GetService("TextChatService"):FindFirstChild("TextChannels"):FindFirstChild("RBXGeneral"); if c then c:SendAsync(text) end else local ce = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents"); if ce then ce.SayMessageRequest:FireServer(text, "All") end end end) end

local TrollTab = Window:CreateTab("冷笑スパム", 4483362458)
local spamDropdown = TrollTab:CreateDropdown({ Name = "ターゲット (表示名)", Options = UpdatePlayerLists(), CurrentOption = {}, MultipleOptions = false, Flag = "SpamTarget", Callback = function(o) targetDisplayName = o[1] or ""; targetPlayerName = ""; for _, p in Players:GetPlayers() do if p.DisplayName == targetDisplayName then targetPlayerName = p.DisplayName; break end end end })
TrollTab:CreateButton({ Name = "🔄 リスト更新", Callback = function() spamDropdown:Refresh(UpdatePlayerLists(), true) end })
TrollTab:CreateToggle({ Name = "スパム開始/停止", CurrentValue = false, Flag = "SpamToggle", Callback = function(v) spamEnabled = v end })

RunService.Heartbeat:Connect(function(dt)
    if spamEnabled and targetPlayerName ~= "" then
        spamTimer = spamTimer + dt
        if spamTimer >= 0.9 then
            spamTimer = 0
            local msg = allMessages[currentIndex]
            currentIndex = currentIndex + 1
            if currentIndex > #allMessages then currentIndex = 1 end
            sendChat(targetPlayerName .. " " .. msg)
        end
    end
end)

-- キック (Kick Hub 公式ロジック)
local selectedPlayer, friendProtection, autoKickTargetActive, isKickAllActive, kickAllLoopActive = nil, false, false, false, false

local noblob_lag_on, noblob_lag_thread = false, nil
local function NoblobStartLag()
    if noblob_lag_on then return end
    noblob_lag_on = true
    noblob_lag_thread = coroutine.create(function()
        local ge = ReplicatedStorage:FindFirstChild("GrabEvents"); if not ge then return end
        local cl = ge:FindFirstChild("CreateGrabLine"); if not cl then return end
        while noblob_lag_on do
            local sp = Workspace:FindFirstChild("SpawnLocation") or Workspace:FindFirstChild("Spawn") or (LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart"))
            if sp then
                local rx, rz = math.random(-1e9,1e9), math.random(-1e9,1e9)
                for _, pos in pairs({CFrame.new(rx,0,rz), CFrame.new(-rx,0,-rz), CFrame.new(rx,0,-rz), CFrame.new(-rx,0,rz)}) do
                    pcall(function() cl:FireServer(sp, pos) end)
                end
            end
            task.wait()
        end
    end)
    coroutine.resume(noblob_lag_thread)
end
local function NoblobStopLag() noblob_lag_on = false; if noblob_lag_thread then coroutine.close(noblob_lag_thread); noblob_lag_thread = nil end end

local function executeBlobmanKickTargetV2(targetName)
    local target = Players:FindFirstChild(targetName)
    if not target or isFriend(target) then return end
    NoblobStartLag(); task.wait(0.5)
    local rootPart = getMyRoot()
    if rootPart then SpawnToyRemoteFunction:InvokeServer("CreatureBlobman", rootPart.CFrame*CFrame.new(0,0,-5), Vector3.new(0,127,0)) end
    task.wait(0.5)
    local toyFolder = Workspace:FindFirstChild(LocalPlayer.Name.."SpawnedInToys")
    local blob = toyFolder and toyFolder:FindFirstChild("CreatureBlobman")
    if not blob then NoblobStopLag(); return end
    local seat = blob:FindFirstChild("VehicleSeat")
    if seat and LocalPlayer.Character then local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid"); if hum then seat:Sit(hum) end end
    task.wait(0.3)
    local myRoot = getMyRoot()
    if not myRoot then NoblobStopLag(); return end
    local targetRoot = target.Character and target.Character:FindFirstChild("HumanoidRootPart")
    if targetRoot and targetRoot.Parent and blob.Parent then
        myRoot.CFrame = targetRoot.CFrame; myRoot.AssemblyAngularVelocity = Vector3.zero; task.wait(0.025)
        if (myRoot.Position - targetRoot.Position).Magnitude <= 35 then
            for i = 1, 25 do
                if not targetRoot.Parent or not blob.Parent then break end
                pcall(function() blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.LeftDetector, targetRoot, blob.LeftDetector.LeftWeld); blob.BlobmanSeatAndOwnerScript.CreatureRelease:FireServer(blob.LeftDetector.LeftWeld) end)
                task.wait(0.01)
            end
        end
    end
    myRoot.CFrame = CFrame.new(0,100,0); myRoot.AssemblyLinearVelocity = Vector3.zero; task.wait(0.1)
    for _, p in ipairs(blob:GetDescendants()) do if p:IsA("BasePart") then pcall(function() p.Anchored = true end) end end
    task.wait(0.1)
    if targetRoot then targetRoot.CFrame = CFrame.new(0,110,0); targetRoot.AssemblyLinearVelocity, targetRoot.AssemblyAngularVelocity = Vector3.zero, Vector3.zero end
    task.wait(0.1)
    if targetRoot then for _ = 1, 2 do task.spawn(function() pcall(function() SetNetworkOwner:FireServer(targetRoot, CFrame.new(targetRoot.Position)); DestroyGrabLine:FireServer(targetRoot) end) end); task.wait(0.1) end end
    task.wait(0.3)
    if targetRoot and blob.Parent then task.spawn(function() pcall(function() blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.LeftDetector, targetRoot, blob.LeftDetector.LeftWeld); blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.RightDetector, targetRoot, blob.RightDetector.RightWeld) end) end) end
    task.wait(0.1)
    for _, p in ipairs(blob:GetDescendants()) do if p:IsA("BasePart") then pcall(function() p.Anchored = false end) end end
    task.wait(0.5)
    if blob and blob.Parent then DestroyToy:FireServer(blob) end
    NoblobStopLag()
end

local function ExecuteBlobKickAllV2()
    if isKickAllActive then return end
    isKickAllActive = true
    NoblobStartLag(); task.wait(0.5)
    local allPlayers = {}
    for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer and not isFriend(p) then table.insert(allPlayers, p) end end
    if #allPlayers == 0 then NoblobStopLag(); isKickAllActive = false; return end
    local rootPart = getMyRoot()
    if rootPart then SpawnToyRemoteFunction:InvokeServer("CreatureBlobman", rootPart.CFrame*CFrame.new(0,0,-5), Vector3.new(0,127,0)) end
    task.wait(0.5)
    local toyFolder = Workspace:FindFirstChild(LocalPlayer.Name.."SpawnedInToys")
    local blob = toyFolder and toyFolder:FindFirstChild("CreatureBlobman")
    if not blob then NoblobStopLag(); isKickAllActive = false; return end
    local seat = blob:FindFirstChild("VehicleSeat")
    if seat and LocalPlayer.Character then local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid"); if hum then seat:Sit(hum) end end
    task.wait(0.3)
    local myRoot = getMyRoot()
    if not myRoot then NoblobStopLag(); isKickAllActive = false; return end
    for _, tp in ipairs(allPlayers) do
        local tr = tp.Character and tp.Character:FindFirstChild("HumanoidRootPart")
        if tr and tr.Parent and blob.Parent then
            myRoot.CFrame = tr.CFrame; myRoot.AssemblyAngularVelocity = Vector3.zero; task.wait(0.02)
            if (myRoot.Position - tr.Position).Magnitude <= 35 then
                for i = 1, 25 do
                    if not tr.Parent or not blob.Parent then break end
                    pcall(function() blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.LeftDetector, tr, blob.LeftDetector.LeftWeld); blob.BlobmanSeatAndOwnerScript.CreatureRelease:FireServer(blob.LeftDetector.LeftWeld) end)
                    task.wait(0.01)
                end
            end
        end
    end
    myRoot.CFrame = CFrame.new(0,100,0); myRoot.AssemblyLinearVelocity = Vector3.zero; task.wait(0.1)
    for _, p in ipairs(blob:GetDescendants()) do if p:IsA("BasePart") then pcall(function() p.Anchored = true end) end end
    task.wait(0.1)
    local radius = 15
    for i, tp in ipairs(allPlayers) do
        local tr = tp.Character and tp.Character:FindFirstChild("HumanoidRootPart")
        if tr then local a = math.rad((i-1)*(360/#allPlayers)); tr.CFrame = CFrame.new(radius*math.cos(a),110,radius*math.sin(a)); tr.AssemblyLinearVelocity, tr.AssemblyAngularVelocity = Vector3.zero, Vector3.zero end
    end
    task.wait(0.1)
    for _ = 1, 2 do for _, tp in ipairs(allPlayers) do local tr = tp.Character and tp.Character:FindFirstChild("HumanoidRootPart"); if tr then task.spawn(function() pcall(function() SetNetworkOwner:FireServer(tr, CFrame.new(tr.Position)); DestroyGrabLine:FireServer(tr) end) end) end end; task.wait(0.1) end
    task.wait(0.3)
    for _, tp in ipairs(allPlayers) do local tr = tp.Character and tp.Character:FindFirstChild("HumanoidRootPart"); if tr and blob.Parent then task.spawn(function() pcall(function() blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.LeftDetector, tr, blob.LeftDetector.LeftWeld); blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.RightDetector, tr, blob.RightDetector.RightWeld) end) end) end end
    task.wait(0.1)
    for _, p in ipairs(blob:GetDescendants()) do if p:IsA("BasePart") then pcall(function() p.Anchored = false end) end end
    task.wait(0.5)
    if blob and blob.Parent then DestroyToy:FireServer(blob) end
    NoblobStopLag(); isKickAllActive = false
end

local function ExecuteBlobKickAllLoop()
    if isKickAllActive then return end
    isKickAllActive = true
    local myRoot = getMyRoot()
    if not myRoot then isKickAllActive = false; return end
    local toyFolder = Workspace:FindFirstChild(LocalPlayer.Name.."SpawnedInToys")
    local blob = toyFolder and toyFolder:FindFirstChild("CreatureBlobman")
    if not blob then
        SpawnToyRemoteFunction:InvokeServer("CreatureBlobman", myRoot.CFrame*CFrame.new(0,0,-5), Vector3.new(0,127,0))
        task.wait(0.5)
        blob = toyFolder and toyFolder:FindFirstChild("CreatureBlobman")
        if not blob then isKickAllActive = false; return end
        local seat = blob:FindFirstChild("VehicleSeat")
        if seat and LocalPlayer.Character then local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid"); if hum then seat:Sit(hum) end end
        task.wait(0.3)
    end
    local allPlayers = {}
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and not isFriend(p) and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then table.insert(allPlayers, p) end
    end
    if #allPlayers == 0 then isKickAllActive = false; return end
    for _, tp in ipairs(allPlayers) do
        if not blob.Parent then break end
        local tr = tp.Character and tp.Character:FindFirstChild("HumanoidRootPart")
        if tr and tr.Parent then
            myRoot = getMyRoot()
            if not myRoot then break end
            myRoot.CFrame = tr.CFrame; task.wait(0.02)
            for i = 1, 25 do if not tr.Parent or not blob.Parent then break end; pcall(function() blob.BlobmanSeatAndOwnerScript.CreatureGrab:FireServer(blob.LeftDetector, tr, blob.LeftDetector.LeftWeld); blob.BlobmanSeatAndOwnerScript.CreatureRelease:FireServer(blob.LeftDetector.LeftWeld) end); task.wait(0.01) end
        end
    end
    isKickAllActive = false
end

local function KickAllNoBlob()
    if isKickAllActive then return end
    isKickAllActive = true
    task.spawn(function()
        NoblobStartLag(); task.wait(1)
        local plrs = {}
        for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer and not isFriend(p) then table.insert(plrs, p) end end
        if #plrs == 0 then NoblobStopLag(); isKickAllActive = false; return end
        local mc, mh = LocalPlayer.Character, LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if not mh then NoblobStopLag(); isKickAllActive = false; return end
        local pd = {}
        for _, p in ipairs(plrs) do local c, h = p.Character, p.Character and p.Character:FindFirstChild("HumanoidRootPart"); if h then table.insert(pd, {plr=p, hrp=h}) end end
        if #pd == 0 then NoblobStopLag(); isKickAllActive = false; return end
        local ge = ReplicatedStorage:FindFirstChild("GrabEvents")
        local so, dl, cl = ge and ge:FindFirstChild("SetNetworkOwner"), ge and ge:FindFirstChild("DestroyGrabLine"), ge and ge:FindFirstChild("CreateGrabLine")
        for _, d in ipairs(pd) do pcall(function() mh.CFrame = d.hrp.CFrame*CFrame.new(0,5,5); mh.AssemblyLinearVelocity = Vector3.zero end); task.wait(0.05); if so and d.hrp then pcall(function() so:FireServer(d.hrp, d.hrp.CFrame) end) end; task.wait() end
        local rad, astep = 40, (math.pi*2)/#pd
        for i, d in ipairs(pd) do local a = (i-1)*astep; local x, z = math.cos(a)*rad, math.sin(a)*rad; pcall(function() d.hrp.CFrame = CFrame.new(x,35,z); d.hrp.AssemblyLinearVelocity, d.hrp.AssemblyAngularVelocity = Vector3.zero, Vector3.zero end); local bp = Instance.new("BodyPosition", d.hrp); bp.MaxForce = Vector3.new(1e9,1e9,1e9); bp.P = 40000000; bp.Position = Vector3.new(x,35,z); d.bp = bp; task.wait() end
        for i = 1, 5 do for _, d in ipairs(pd) do if cl and d.hrp and d.hrp.Parent then pcall(function() cl:FireServer(d.hrp, CFrame.new(math.random(-1e9,1e9), math.random(1e5,1e9), math.random(-1e9,1e9))) end) end end; task.wait(0.05) end
        for _, d in ipairs(pd) do if dl and d.hrp and d.hrp.Parent then pcall(function() dl:FireServer(d.hrp) end) end end
        task.wait(0.1)
        for i = 1, 3 do for _, d in ipairs(pd) do if cl and d.hrp and d.hrp.Parent then pcall(function() cl:FireServer(d.hrp, CFrame.new(math.random(-1e9,1e9), math.random(1e5,1e9), math.random(-1e9,1e9))) end) end end; task.wait(0.05) end
        for i = 1, 5 do for _, d in ipairs(pd) do if d.hrp and d.hrp.Parent then pcall(function() d.hrp.CFrame = d.hrp.CFrame + Vector3.new(math.random(-500,500), math.random(100,500), math.random(-500,500)); d.hrp.AssemblyLinearVelocity, d.hrp.AssemblyAngularVelocity = Vector3.zero, Vector3.zero end) end end; task.wait(0.1) end
        for _, d in ipairs(pd) do if d.hrp and d.hrp.Parent then pcall(function() d.hrp.CFrame = CFrame.new(math.random(-99999,99999), math.random(500,99999), math.random(-99999,99999)); d.hrp.AssemblyLinearVelocity, d.hrp.AssemblyAngularVelocity = Vector3.zero, Vector3.zero; if d.bp then pcall(function() d.bp:Destroy() end); d.bp = nil end end) end end
        task.wait(0.1)
        for i = 1, 3 do for _, d in ipairs(pd) do if so and dl and d.hrp and d.hrp.Parent then pcall(function() so:FireServer(d.hrp, d.hrp.CFrame); task.wait(0.01); dl:FireServer(d.hrp) end) end end; task.wait(0.05) end
        NoblobStopLag(); isKickAllActive = false
    end)
end

local KickTab = Window:CreateTab("キック", 4483362458)
local KickDropdown = KickTab:CreateDropdown({ Name = "キック対象 (表示名)", Options = UpdatePlayerLists(), CurrentOption = {}, MultipleOptions = false, Flag = "KickTarget", Callback = function(o) local dn = o[1] or ""; selectedPlayer = nil; for _, p in Players:GetPlayers() do if p.DisplayName == dn then selectedPlayer = p.Name; break end end end })
KickTab:CreateButton({ Name = "🔄 リスト更新", Callback = function() KickDropdown:Refresh(UpdatePlayerLists(), true) end })
KickTab:CreateToggle({ Name = "フレンド保護", CurrentValue = false, Flag = "FriendProtect", Callback = function(v) friendProtection = v end })
KickTab:CreateButton({ Name = "🎯 ターゲットをキック", Callback = function() if selectedPlayer then task.spawn(function() executeBlobmanKickTargetV2(selectedPlayer) end) end end })
KickTab:CreateToggle({ Name = "🔁 ターゲット自動キック", CurrentValue = false, Flag = "AutoKickTarget", Callback = function(v) autoKickTargetActive = v; if v then task.spawn(function() while autoKickTargetActive do if selectedPlayer then local t = Players:FindFirstChild(selectedPlayer); if t and not isFriend(t) then executeBlobmanKickTargetV2(selectedPlayer) end end; task.wait(0.5) end end) end end })
KickTab:CreateButton({ Name = "💀 全員キック", Callback = function() task.spawn(ExecuteBlobKickAllV2) end })
KickTab:CreateButton({ Name = "🚫 全員キック (No-Blob)", Callback = function() task.spawn(KickAllNoBlob) end })
KickTab:CreateToggle({ Name = "🔁 全員キック ループ", CurrentValue = false, Flag = "KickAllLoop", Callback = function(v) kickAllLoopActive = v; if v then task.spawn(function() while kickAllLoopActive do if not isKickAllActive then ExecuteBlobKickAllLoop() end; task.wait(0.1) end end) end end })

-- Pallet Ride
local PalletRideEnabled, PalletRideTask, PalletRideCurrentPallet, PalletRideHeight = false, nil, nil, 3
local function SpawnPallet() local char = LocalPlayer.Character; if not char then return nil end; local hrp = char:FindFirstChild("HumanoidRootPart"); if not hrp then return nil end; local cam = Workspace.CurrentCamera; local pos = hrp.Position + Vector3.new(0, 2, 0); local cf = CFrame.new(pos) * (cam.CFrame - cam.CFrame.Position); local tf = Workspace:FindFirstChild(LocalPlayer.Name .. "SpawnedInToys"); local bl = {}; if tf then for _, o in ipairs(tf:GetChildren()) do if o.Name == "PalletLightBrown" then bl[o] = true end end end; pcall(function() SpawnToyRemoteFunction:InvokeServer("PalletLightBrown", cf, Vector3.new(0, 89, 0)) end); local np = nil; local t = tick() + 3; while tick() < t do local tf2 = Workspace:FindFirstChild(LocalPlayer.Name .. "SpawnedInToys"); if tf2 then for _, o in ipairs(tf2:GetChildren()) do if o.Name == "PalletLightBrown" and not bl[o] then np = o; break end end end; if np then break end; task.wait(0.05) end; return np end
local function GetPalletTopPart(p) if not p then return nil end; local t = p:FindFirstChild("Main") or p:FindFirstChildWhichIsA("BasePart"); if t then return t end; for _, x in ipairs(p:GetDescendants()) do if x:IsA("BasePart") then return x end end; return nil end
local function AttachToPallet() local c = LocalPlayer.Character; if not c then return false end; local h = c:FindFirstChild("HumanoidRootPart"); if not h then return false end; local p = PalletRideCurrentPallet; if not p or not p.Parent then return false end; local t = GetPalletTopPart(p); if not t then return false end; local cf = t.CFrame * CFrame.new(0, t.Size.Y / 2 + PalletRideHeight, 0); h.CFrame = cf; h.AssemblyLinearVelocity = Vector3.zero; h.AssemblyAngularVelocity = Vector3.zero; return true end
local function StartPalletRide() if PalletRideEnabled then return end; PalletRideEnabled = true; PalletRideTask = task.spawn(function() PalletRideCurrentPallet = SpawnPallet(); if not PalletRideCurrentPallet then PalletRideEnabled = false; return end; task.wait(0.3); AttachToPallet(); while PalletRideEnabled do local p = PalletRideCurrentPallet; if not p or not p.Parent then PalletRideCurrentPallet = SpawnPallet(); if not PalletRideCurrentPallet then task.wait(0.5); continue end; task.wait(0.3); AttachToPallet() else local c = LocalPlayer.Character; local h = c and c:FindFirstChild("HumanoidRootPart"); if h then local t = GetPalletTopPart(p); if t then local cf = t.CFrame * CFrame.new(0, t.Size.Y / 2 + PalletRideHeight, 0); h.CFrame = cf; h.AssemblyLinearVelocity = Vector3.zero; h.AssemblyAngularVelocity = Vector3.zero end end end; RunService.Heartbeat:Wait() end end) end
local function StopPalletRide() PalletRideEnabled = false; if PalletRideTask then task.cancel(PalletRideTask); PalletRideTask = nil end; PalletRideCurrentPallet = nil end

local PalletTab = Window:CreateTab("Pallet Ride", 4483362458)
PalletTab:CreateToggle({ Name = "Pallet Ride", CurrentValue = false, Flag = "PalletToggle", Callback = function(v) if v then StartPalletRide() else StopPalletRide() end end })
PalletTab:CreateSlider({ Name = "高さ", Range = {1, 20}, Increment = 1, Suffix = " studs", CurrentValue = 3, Flag = "PalletHeight", Callback = function(v) PalletRideHeight = v end })

-- Server Crash
local CrashTab = Window:CreateTab("サーバークラッシュ", 4483362458)
CrashTab:CreateButton({ Name = "クラッシュ", Callback = function() local RS = game:GetService("ReplicatedStorage"); local U = RS.DataEvents.UpdateTexturesChoice; if U then task.spawn(function() pcall(function() U:FireServer(string.rep("A", 5e6)) end) end) end; local D = RS.DataEvents.DataRemoteEvent; if D then task.spawn(function() local c = 0; while true do for _ = 1, 50 do pcall(function() D:FireServer() end) end; c = c + 50; if c >= 1e6 then break end; task.wait(0.05) end end) end end })

-- Player Tab
local PlayerTab = Window:CreateTab("プレイヤー", 4483362458)
local Camera = Workspace.CurrentCamera
PlayerTab:CreateToggle({ Name = "三人称", CurrentValue = false, Flag = "ThirdPerson", Callback = function(v) local char = LocalPlayer.Character; if not char then return end; local hum = char:FindFirstChildOfClass("Humanoid"); if v then LocalPlayer.CameraMode = Enum.CameraMode.Classic; LocalPlayer.CameraMaxZoomDistance = 16456456546; LocalPlayer.CameraMinZoomDistance = 0.5 else LocalPlayer.CameraMode = Enum.CameraMode.LockFirstPerson; LocalPlayer.CameraMaxZoomDistance = 0; LocalPlayer.CameraMinZoomDistance = 0 end end })
local infJumpConn = nil
PlayerTab:CreateToggle({ Name = "インフィニティジャンプ", CurrentValue = false, Flag = "InfiniteJump", Callback = function(v) if infJumpConn then infJumpConn:Disconnect(); infJumpConn = nil end; if v then infJumpConn = game:GetService("UserInputService").JumpRequest:Connect(function() local c = LocalPlayer.Character; local h = c and c:FindFirstChildOfClass("Humanoid"); if h then h:ChangeState(Enum.HumanoidStateType.Jumping) end end) end end })

local espEnabled, espHighlights, espBillboards = false, {}, {}
local function CreateESP(player) if not player or player == LocalPlayer then return end; if espHighlights[player] then return end; local char = player.Character; if not char then return end; local h = Instance.new("Highlight"); h.Name = "PlayerESP"; h.Adornee = char; h.FillColor = Color3.fromRGB(255, 0, 0); h.FillTransparency = 0.5; h.OutlineColor = Color3.fromRGB(255, 255, 255); h.Parent = char; espHighlights[player] = h; local head = char:FindFirstChild("Head"); if head then local b = Instance.new("BillboardGui"); b.Name = "ESPName"; b.Adornee = head; b.Size = UDim2.new(0, 200, 0, 50); b.StudsOffset = Vector3.new(0, 2.5, 0); b.AlwaysOnTop = true; b.Parent = head; local l = Instance.new("TextLabel"); l.Size = UDim2.new(1, 0, 1, 0); l.BackgroundTransparency = 1; l.TextColor3 = Color3.fromRGB(255, 255, 255); l.TextStrokeTransparency = 0; l.Font = Enum.Font.GothamBold; l.TextSize = 16; l.Text = player.Name; l.Parent = b; espBillboards[player] = b end end
local function RemoveESP(player) if espHighlights[player] then pcall(function() espHighlights[player]:Destroy() end); espHighlights[player] = nil end; if espBillboards[player] then pcall(function() espBillboards[player]:Destroy() end); espBillboards[player] = nil end end
PlayerTab:CreateToggle({ Name = "プレイヤーESP", CurrentValue = false, Flag = "PlayerESP", Callback = function(v) espEnabled = v; if v then for _, p in ipairs(Players:GetPlayers()) do CreateESP(p) end else for _, p in ipairs(Players:GetPlayers()) do RemoveESP(p) end end end })
RunService.Heartbeat:Connect(function() if not espEnabled then return end; for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer and p.Character then if not espHighlights[p] then CreateESP(p) end; local b = espBillboards[p]; if b and b.Parent then local l = b:FindFirstChildOfClass("TextLabel"); if l and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then l.Text = p.Name .. " [" .. math.floor(p:DistanceFromCharacter(LocalPlayer.Character.HumanoidRootPart.Position)) .. "m]" end end else RemoveESP(p) end end end)

-- Toy Tab
local ToyTab = Window:CreateTab("トイ", 4483362458)
local SnipeConfig = { TargetPlayer = nil, LoopKill = false }
local function SnipeMoveTo(part, targetCFrame) if not part or not part.Parent then return end; local b = Instance.new("BodyPosition"); b.MaxForce = Vector3.new(1e8, 1e8, 1e8); b.Position = targetCFrame.Position; b.P = 2e4; b.D = 5e3; b.Parent = part end
local function SnipeVelocity(part, vel) if not part or not part.Parent then return end; local bv = Instance.new("BodyVelocity"); bv.MaxForce = Vector3.new(1e8, 1e8, 1e8); bv.Velocity = vel; bv.Parent = part; Debris:AddItem(bv, 1) end
local function Snipefunc(root, func) if not root or not root.Parent then return end; local hrp = getMyRoot(); if not hrp then return end; task.spawn(function() Workspace.CurrentCamera.CFrame = CFrame.lookAt(Workspace.CurrentCamera.CFrame.Position, root.Position); for _ = 1, 4 do local h = getMyRoot(); if h then SetNetworkOwner:FireServer(root, h.CFrame) end; task.wait(0.05) end; func() end) end
local function SnipeKill(target) local c = target.Character; local root = c and c:FindFirstChild("HumanoidRootPart"); if root then Snipefunc(root, function() SnipeMoveTo(root, CFrame.new(4096, -75, 4096)); SnipeVelocity(root, Vector3.new(0, -1000, 0)) end) end end
local snipeDropdown = ToyTab:CreateDropdown({ Name = "Snipeターゲット", Options = UpdatePlayerLists(), CurrentOption = {}, Flag = "SnipeTarget", Callback = function(o) local dn = o[1] or ""; for _, p in Players:GetPlayers() do if p.DisplayName == dn then SnipeConfig.TargetPlayer = p; break end end end })
ToyTab:CreateButton({ Name = "🔄 リスト更新", Callback = function() snipeDropdown:Refresh(UpdatePlayerLists(), true) end })
ToyTab:CreateToggle({ Name = "Loop Kill", CurrentValue = false, Flag = "SnipeKill", Callback = function(v) SnipeConfig.LoopKill = v; if v then task.spawn(function() while SnipeConfig.LoopKill do if SnipeConfig.TargetPlayer and SnipeConfig.TargetPlayer.Character then SnipeKill(SnipeConfig.TargetPlayer) end; task.wait(1.5) end end) end end })

-- Barrier Break
local BarrierTab = Window:CreateTab("バリア破壊", 4483362458)
local function executeBarrierBreak() local h = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid"); if not h then return end; local origCF = LocalPlayer.Character.HumanoidRootPart.CFrame; h.WalkSpeed = 0; ReplicatedStorage.MenuToys.SpawnToyRemoteFunction:InvokeServer("InstrumentWoodwindOcarina", CFrame.new(184.148834, -5.54824972, 498.136749, 0.829037189, -0.214714944, 0.516328275, 0, 0.923344612, 0.383972496, -0.559193552, -0.318327487, 0.765486956), Vector3.new(0, 34, 0)); task.wait(0.4); local tf = Workspace:FindFirstChild(LocalPlayer.Name.."SpawnedInToys"); local oc = tf and tf:FindFirstChild("InstrumentWoodwindOcarina"); if oc then oc.HoldPart.HoldItemRemoteFunction:InvokeServer(oc, Workspace[LocalPlayer.Name]); LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(304.06, 25.77, 488.54); task.wait(0.21); ReplicatedStorage.MenuToys.DestroyToy:FireServer(oc); LocalPlayer.Character.HumanoidRootPart.CFrame = origCF; task.wait(0.7); ReplicatedStorage.MenuToys.SpawnToyRemoteFunction:InvokeServer("Campfire", CFrame.new(257.638672, -5.57392979, 450.103638, -0.950906992, -0.171067372, 0.257899135, 0, 0.833338678, 0.552762806, -0.309477001, 0.525626004, -0.79242748), Vector3.new(0, 161.9720001220703, 0)); task.wait(0.7) end; h.WalkSpeed = 16 end
BarrierTab:CreateButton({ Name = "Break Barrier", Callback = function() executeBarrierBreak() end })

-- Backpack (おんぶ)
local BackpackTab = Window:CreateTab("おんぶ", 4483362458)
local selectedTargetName2 = ""
local targetDropdown2 = BackpackTab:CreateDropdown({ Name = "ターゲット", Options = (function() local t = {}; for _, p in Players:GetPlayers() do if p ~= LocalPlayer then table.insert(t, p.Name) end end; return t end)(), CurrentOption = {}, Flag = "BackpackTarget", Callback = function(o) selectedTargetName2 = o[1] or "" end })
BackpackTab:CreateButton({ Name = "🔄 リスト更新", Callback = function() local t = {}; for _, p in Players:GetPlayers() do if p ~= LocalPlayer then table.insert(t, p.Name) end end; targetDropdown2:Refresh(t, true) end })
BackpackTab:CreateButton({ Name = "おんぶ実行 (簡易)", Callback = function() local target = Players:FindFirstChild(selectedTargetName2); if not target or not target.Character then return end; local tr = target.Character:FindFirstChild("HumanoidRootPart"); local mr = getMyRoot(); if not tr or not mr then return end; SetNetworkOwner:FireServer(tr, mr.CFrame); task.wait(0.1); tr.CFrame = mr.CFrame * CFrame.new(0, 1, 1.5); tr.CFrame = mr.CFrame * CFrame.new(0, 1, 1.5) end })

-- ============================================================
-- Piano Tab (Inferno 修正版)
-- ============================================================
local PianoTab = Window:CreateTab("ピアノ", 4483362458)
local pianoEnabled, pianoFollowEnabled = false, true
local pianoKeyboard = nil
local isPlayingSong = false
local pianoUpdateConnection = nil
local pianoOriginalCollisions = {}

local InfernoData = {
    {key="Key2E", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2B", delay=0.32}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2E", delay=0.32},
    {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16},
    {key="Key2E", delay=0.32}, {key="Key2Fsharp", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key1Dsharp", delay=0.32}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16},
    {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16},
    {key="Key2E", delay=0.32}, {key="Key1Dsharp", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.64},
    {key="Key2B", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16},
    {key="Key2E", delay=0.32}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.32},
    {key="Key2A", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16},
    {key="Key2B", delay=0.32}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.64},
    {key="Key3C", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16},
    {key="Key2B", delay=0.32}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.64},
    {key="Key2E", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2B", delay=0.32}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2E", delay=0.32},
    {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.32}, {key="Key2Fsharp", delay=0.32}, {key="Key2E", delay=0.32},
    {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16},
    {key="Key2E", delay=0.32}, {key="Key1Dsharp", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.64},
    {key="Key2B", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16},
    {key="Key3E", delay=0.32}, {key="Key3Dsharp", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.32},
    {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2B", delay=0.16},
    {key="Key2E", delay=0.32}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.32},
    {key="Key2E", delay=0.16}, {key="Key2E", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2A", delay=0.32}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.16}, {key="Key2E", delay=0.32},
    {key="Key2B", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key3Dsharp", delay=0.16}, {key="Key3E", delay=0.32}, {key="Key3Dsharp", delay=0.16}, {key="Key3C", delay=0.16}, {key="Key2B", delay=0.32},
    {key="Key3C", delay=0.16}, {key="Key2B", delay=0.16}, {key="Key2A", delay=0.16}, {key="Key2Gsharp", delay=0.16}, {key="Key2Fsharp", delay=0.32}, {key="Key2E", delay=0.32}, {key="Key1Dsharp", delay=0.32}
}

local function getMusicKeyboard()
    local myName = LocalPlayer.Name
    local spawnedToys = Workspace:FindFirstChild(myName .. "SpawnedInToys")
    if spawnedToys then
        local kb = spawnedToys:FindFirstChild("MusicKeyboard")
        if kb then return kb end
    end
    for _, item in ipairs(Workspace:GetChildren()) do
        if item.Name == "MusicKeyboard" and item:IsA("Model") then
            local ownerValue = item:FindFirstChild("Owner") or item:FindFirstChild("PartOwner")
            if ownerValue and ownerValue:IsA("StringValue") and ownerValue.Value == myName then
                return item
            end
        end
    end
    return nil
end

local function stopPiano()
    if pianoUpdateConnection then pianoUpdateConnection:Disconnect(); pianoUpdateConnection = nil end
    if pianoKeyboard and pianoKeyboard.Parent then
        local pp = pianoKeyboard:FindFirstChild("Main", true) or pianoKeyboard.PrimaryPart
        if not pp then return end
        for _, child in ipairs(pp:GetChildren()) do
            if child:IsA("Attachment") or child:IsA("AlignPosition") or child:IsA("AlignOrientation") then child:Destroy() end
        end
    end
    for part, canCollide in pairs(pianoOriginalCollisions) do
        if part and part.Parent then part.CanCollide = canCollide end
    end
    pianoOriginalCollisions = {} 
end

local function setupPianoFollow()
    if not pianoKeyboard then pianoKeyboard = getMusicKeyboard() end
    if not pianoKeyboard then return end
    if pianoUpdateConnection then return end
    local mainPart = pianoKeyboard:FindFirstChild("Main", true) or pianoKeyboard.PrimaryPart
    if not mainPart then return end
    
    for _, part in ipairs(pianoKeyboard:GetDescendants()) do
        if part:IsA("BasePart") then
            if pianoOriginalCollisions[part] == nil then pianoOriginalCollisions[part] = part.CanCollide end
            part.CanCollide = false; part.CanTouch = false; part.CanQuery = false
            part.Anchored = false; part.Massless = true
            part.AssemblyLinearVelocity = Vector3.zero; part.AssemblyAngularVelocity = Vector3.zero
            pcall(function() part:SetNetworkOwner(LocalPlayer) end)
        end
    end
    
    local pp = mainPart
    local char = LocalPlayer.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    if root then
        local offset = CFrame.new(0, -1.5, -2) * CFrame.Angles(0, math.rad(180), 0)
        pp.CFrame = root.CFrame * offset
    end
    
    local a0 = Instance.new("Attachment", pp)
    local ap = Instance.new("AlignPosition", pp)
    ap.Attachment0 = a0; ap.Mode = Enum.PositionAlignmentMode.OneAttachment; ap.MaxForce = 1e9; ap.Responsiveness = 200
    local ao = Instance.new("AlignOrientation", pp)
    ao.Attachment0 = a0; ao.Mode = Enum.OrientationAlignmentMode.OneAttachment; ao.MaxTorque = 1e9; ao.Responsiveness = 200
    
    pianoUpdateConnection = RunService.RenderStepped:Connect(function()
        local char = LocalPlayer.Character
        local root = char and char:FindFirstChild("HumanoidRootPart")
        if not root then return end
        if not pianoKeyboard or not pianoKeyboard.Parent then stopPiano(); return end
        if math.random() < 0.05 then pcall(function() pp:SetNetworkOwner(LocalPlayer) end) end
        local offset = CFrame.new(0, -1.5, -2) * CFrame.Angles(0, math.rad(180), 0)
        local targetCF = root.CFrame * offset
        ap.Position = targetCF.Position; ao.CFrame = targetCF
    end)
end

local function pressPianoKey(keyName)
    local targetKeyboard = getMusicKeyboard()
    if not targetKeyboard then return end
    local key = targetKeyboard:FindFirstChild(keyName, true)
    if key and key:IsA("BasePart") then
        SetNetworkOwner:FireServer(key, key.CFrame)
        task.wait(0.08)
    end
end

local function playSongFromJSON(songData)
    if isPlayingSong then return end
    if type(songData) ~= "table" then return end

    isPlayingSong = true
    task.spawn(function()
        if not pianoKeyboard then pianoKeyboard = getMusicKeyboard() end
        for i, note in ipairs(songData) do
            if not isPlayingSong then break end
            local keyName = tostring(note.key)
            local delayTime = note.delay or 0.1
            task.spawn(function() pressPianoKey(keyName) end)
            task.wait(delayTime)
        end
        isPlayingSong = false
    end)
end

PianoTab:CreateToggle({ Name = "ピアノ機能を有効化", CurrentValue = false, Flag = "PianoEnable", Callback = function(v)
    pianoEnabled = v
    if v then
        pianoKeyboard = getMusicKeyboard()
        if pianoKeyboard then
            if pianoFollowEnabled then setupPianoFollow() end
            Rayfield:Notify({Title = "ピアノ", Content = "MusicKeyboardを検出しました", Duration = 5, Image = 4483362458})
        else
            pianoEnabled = false
            Rayfield:Notify({Title = "エラー", Content = "MusicKeyboardが見つかりません", Duration = 5, Image = 4483362458})
        end
    else
        isPlayingSong = false
        stopPiano()
    end
end })

PianoTab:CreateToggle({ Name = "プレイヤー追従", CurrentValue = true, Flag = "PianoFollow", Callback = function(v)
    pianoFollowEnabled = v
    if pianoEnabled and pianoKeyboard and pianoKeyboard.Parent then
        if v then setupPianoFollow() else stopPiano() end
    elseif pianoEnabled and v then
        pianoKeyboard = getMusicKeyboard()
        if pianoKeyboard then setupPianoFollow() end
    end
end })

PianoTab:CreateButton({ Name = "▶ Inferno を再生", Callback = function()
    if not pianoKeyboard then pianoKeyboard = getMusicKeyboard() end
    if not pianoKeyboard then Rayfield:Notify({Title = "エラー", Content = "MusicKeyboardが見つかりません", Duration = 3, Image = 4483362458}); return end
    playSongFromJSON(InfernoData)
    Rayfield:Notify({Title = "ピアノ", Content = "Inferno 再生開始", Duration = 3, Image = 4483362458})
end })

PianoTab:CreateButton({ Name = "⏹ 停止", Callback = function() isPlayingSong = false end })

Rayfield:Notify({Title="Japan Hub", Content="読み込み完了", Duration=3, Image=4483362458})

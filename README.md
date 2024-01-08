function GetUi() 
    if getgenv().Tvk then
    if game.CoreGui:FindFirstChild("Sea Hub GUI") then
        for a, v in ipairs(game.CoreGui:GetChildren()) do
            if v.Name == "Sea Hub GUI" then
                v:Destroy()
            end
        end
    end
end
getgenv().Tvk = true
getgenv().Chon = true

local oldcolor = {
    ["Border Color"] = Color3.fromRGB(131, 181, 255),
    ["Click Effect Color"] = Color3.fromRGB(230, 230, 230),
    ["Setting Icon Color"] = Color3.fromRGB(230, 230, 230),
    ["Logo Image"] = "rbxassetid://6248942117",
    ["Search Icon Color"] = Color3.fromRGB(255, 255, 255),
    ["Search Icon Highlight Color"] = Color3.fromRGB(131, 181, 255),
    ["GUI Text Color"] = Color3.fromRGB(230, 230, 230),
    ["Text Color"] = Color3.fromRGB(230, 230, 230),
    ["Placeholder Text Color"] = Color3.fromRGB(178, 178, 178),
    ["Title Text Color"] = Color3.fromRGB(131, 181, 255),
    ["Background 1 Color"] = Color3.fromRGB(43, 43, 43),
    ["Background 1 Transparency"] = 0,
    ["Background 2 Color"] = Color3.fromRGB(90, 90, 90),
    ["Background 3 Color"] = Color3.fromRGB(53, 53, 53),
    ["Background Image"] = "",
    ["Page Selected Color"] = Color3.fromRGB(131, 181, 255),
    ["Section Text Color"] = Color3.fromRGB(131, 181, 255),
    ["Section Underline Color"] = Color3.fromRGB(131, 181, 255),
    ["Toggle Border Color"] = Color3.fromRGB(131, 181, 255),
    ["Toggle Checked Color"] = Color3.fromRGB(230, 230, 230),
    ["Toggle Desc Color"] = Color3.fromRGB(185, 185, 185),
    ["Button Color"] = Color3.fromRGB(131, 181, 255),
    ["Label Color"] = Color3.fromRGB(101, 152, 220),
    ["Dropdown Icon Color"] = Color3.fromRGB(230, 230, 230),
    ["Dropdown Selected Color"] = Color3.fromRGB(131, 181, 255),
    ["Textbox Highlight Color"] = Color3.fromRGB(131, 181, 255),
    ["Box Highlight Color"] = Color3.fromRGB(131, 181, 255),
    ["Slider Line Color"] = Color3.fromRGB(75, 75, 75),
    ["Slider Highlight Color"] = Color3.fromRGB(59, 82, 115),
    ["Tween Animation 1 Speed"] = 0.25,
    ["Tween Animation 2 Speed"] = 0.5,
    ["Tween Animation 3 Speed"] = 0.1
}

local b = {
    ["Border Color"] = Color3.fromRGB(255,255,255),
    ["Click Effect Color"] = Color3.fromRGB(230, 230, 230),
    ["Setting Icon Color"] = Color3.fromRGB(230, 230, 230),
    ["Logo Image"] = "rbxassetid://6248942117",
    ["Search Icon Color"] = Color3.fromRGB(255, 255, 255),
    ["Search Icon Highlight Color"] = Color3.fromRGB(142, 172, 255),
    ["GUI Text Color"] = Color3.fromRGB(70, 70, 70),
    ["Text Color"] = Color3.fromRGB(70, 70, 70),
    ["Placeholder Text Color"] = Color3.fromRGB(100, 100, 100),
    ["Title Text Color"] = Color3.fromRGB(142, 172, 255),
    ["Background Main Color"] = Color3.fromRGB(255, 255, 255),
    ["Background 1 Color"] = Color3.fromRGB(220, 220, 220),
    ["Background 1 Transparency"] = 0,
    ["Background 2 Color"] = Color3.fromRGB(200, 200, 200),
    ["Background 3 Color"] = Color3.fromRGB(255, 255, 255),
    ["Background Image"] = "",
    ["Page Selected Color"] = Color3.fromRGB(142, 172, 255),
    ["Section Text Color"] = Color3.fromRGB(142, 172, 255),
    ["Section Underline Color"] = Color3.fromRGB(142, 172, 255),
    ["Toggle Border Color"] = Color3.fromRGB(142, 172, 255),
    ["Toggle Checked Color"] = Color3.fromRGB(70, 70, 70),
    ["Toggle Desc Color"] = Color3.fromRGB(70, 70, 70),
    ["Button Color"] = Color3.fromRGB(142, 172, 255),
    ["Label Color"] = Color3.fromRGB(142, 172, 255),
    ["Dropdown Icon Color"] = Color3.fromRGB(70, 70, 70),
    ["Dropdown Selected Color"] = Color3.fromRGB(142, 172, 255),
    ["Textbox Highlight Color"] = Color3.fromRGB(142, 172, 255),
    ["Box Highlight Color"] = Color3.fromRGB(142, 172, 255),
    ["Slider Line Color"] = Color3.fromRGB(75, 75, 75),
    ["Slider Highlight Color"] = Color3.fromRGB(59, 82, 115),
    ["Tween Animation 1 Speed"] = 0.25,
    ["Tween Animation 2 Speed"] = 0.5,
    ["Tween Animation 3 Speed"] = 0.1
}

local c = {}
for d, v in pairs(b) do
    c[d] = {}
end
local e = {}
for d, v in pairs(b) do
    e[d] = {Color = v, Rainbow = false, Breathing = {Toggle = false, Color1 = Color3.new(), Color2 = Color3.new()}}
end
local function f(g)
    return {math.floor(g.r * 255), math.floor(g.g * 255), math.floor(g.b * 255), "Dit"}
end
function CorrectTable(h)
    local i = {}
    for d, v in pairs(h) do
        if typeof(v) == "Color3" then
            i[d] = f(v)
        elseif type(v) == "table" then
            i[d] = CorrectTable(v)
        else
            i[d] = v
        end
    end
    return i
end
function DCorrectTable(h)
    local i = {}
    for d, v in pairs(h) do
        if type(v) == "table" and v[4] == "Dit" then
            i[d] = Color3.fromRGB(unpack(v))
        elseif type(v) == "table" then
            i[d] = DCorrectTable(v)
        else
            i[d] = v
        end
    end
    return i
end
local j = game:GetService("HttpService")
local k = "!CustomUI.json"
function SaveCustomUISettings()
    local j = game:GetService("HttpService")
    if not isfolder("Sea Hub") then
        makefolder("Sea Hub")
    end
    writefile("Sea Hub/" .. k, j:JSONEncode(CorrectTable(e)))
end
function ReadCustomUISetting()
    local l, m =
        pcall(
        function()
            local j = game:GetService("HttpService")
            if not isfolder("Sea Hub") then
                makefolder("Sea Hub")
            end
            local n = j:JSONDecode(readfile("Sea Hub/" .. k))
            for d, v in pairs(n) do
                local function o()
                    if v.Color == nil then
                        return
                    end
                    if v.Rainbow == nil then
                        return
                    end
                    if v.Breathing == nil then
                        return
                    end
                    if v.Breathing.Color1 == nil then
                        return
                    end
                    if v.Breathing.Color2 == nil then
                        return
                    end
                    return true
                end
                if not o() then
                    SaveCustomUISettings()
                    return ReadCustomUISetting()
                end
            end
            return n
        end
    )
    if l then
        return m
    else
        SaveCustomUISettings()
        return ReadCustomUISetting()
    end
end
if not getgenv().Chon then 
    e = DCorrectTable(ReadCustomUISetting())
    for d, v in pairs(e) do
        b[d] = v.Color
    end
end
if not getgenv().ractvkretarddumb then
    spawn(
        function()
            while wait(1) do
                SaveCustomUISettings()
            end
        end
    )
    getgenv().ractvkretarddumb = true
end
getgenv().UIColor = b
    setmetatable(
    {},
    {__newindex = function(p, q, r)
            if c[q] then
                for d, v in pairs(c[q]) do
                    v()
                end
            end
            rawset(b, q, r)
            if not e[q] then
                e[q] = {
                    Color = v,
                    Rainbow = false,
                    Breathing = {Toggle = false, Color1 = Color3.new(), Color2 = Color3.new()}
                }
            end
            e[q].Color = r
        end, __index = b}
)
local s = {}
local t = {}
local u = {}
local w = game:GetService("TweenService")
local x = game:GetService("UserInputService")
function u.ButtonEffect()
    local y = game:GetService("Players").LocalPlayer:GetMouse()
    local z = Drawing.new("Circle")
    z.Visible = true
    z.Radius = 10
    z.Filled = true
    z.Color = getgenv().UIColor["Click Effect Color"]
    z.Position = Vector2.new(y.X, y.Y + 35)
    local A = Instance.new("Folder")
    A.Parent = u.gui
    A.Name = "Game nhu buoi"
    local n = Instance.new("NumberValue")
    n.Value = 10
    n.Parent = A
    n.Name = "Rua nhu buoi"
    local B = Instance.new("NumberValue")
    B.Value = 1
    B.Parent = A
    B.Name = "Rua nhu buoi 2"
    w:Create(n, TweenInfo.new(.25), {Value = 25}):Play()
    w:Create(B, TweenInfo.new(.25), {Value = 0}):Play()
    n:GetPropertyChangedSignal("Value"):Connect(
        function()
            z.Radius = n.Value
        end
    )
    B:GetPropertyChangedSignal("Value"):Connect(
        function()
            z.Transparency = B.Value
        end
    )
    wait(.5)
    A:Destroy()
end
u.GetIMG = function(C)
    local D = "SynAsset ["
    local E = ""
    if string.find(C, "rbxassetid://") then
        E = C
    else
        pcall(
            function()
                if C and type(C) == "string" and tostring(game:HttpGet(C)):find("PNG") then
                    for a = 1, 5 do
                        D = tostring(D .. string.char(math.random(65, 122)))
                    end
                    D = D .. "].png"
                    writefile(D, game:HttpGet(C))
                    spawn(
                        function()
                            wait(5)
                            delfile(D)
                        end
                    )
                    E = getsynasset(D)
                end
            end
        )
    end
    return E
end
u.Gui = Instance.new("ScreenGui")
u.Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
u.Gui.Name = "Sea Hub GUI"
getgenv().ReadyForGuiLoaded = false
spawn(
    function()
        u.Gui.Enabled = false
        repeat
            wait()
        until getgenv().ReadyForGuiLoaded
        u.Gui.Enabled = true
    end
)
u.NotiGui = Instance.new("ScreenGui")
u.NotiGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
u.NotiGui.Name = "Sea Hub Notification"
local F = Instance.new("Frame")
local G = Instance.new("UIListLayout")
F.Name = "NotiContainer"
F.Parent = u.NotiGui
F.AnchorPoint = Vector2.new(1, 1)
F.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
F.BackgroundTransparency = 1.000
F.Position = UDim2.new(1, -5, 1, -5)
F.Size = UDim2.new(0, 350, 1, -10)
G.Name = "NotiList"
G.Parent = F
G.SortOrder = Enum.SortOrder.LayoutOrder
G.VerticalAlignment = Enum.VerticalAlignment.Bottom
G.Padding = UDim.new(0, 5)
wait()
getgenv().GUI = u.Gui
--syn.unprotect_gui(GUI)
-- // GOOGLE TRANSLATE // --

-- function SetUpTranslate()
--     local YourLang = "vi" -- Language code that the messages are going to be translated to

--     local googlev = isfile'googlev.txt' and readfile'googlev.txt' or ''
--     local request = request or syn.request
    
--     local function outputHook(fnc)
--         return function(...)
--             return fnc('[INLINE TRANSLATOR]', ...)
--         end
--     end
--     local translate, getISOCode do
--         function googleConsent(Body) -- Because google really said: "Fuck you."
--             local args = {}
    
--             for match in Body:gmatch('<input type="hidden" name=".-" value=".-">') do
--                 local k,v = match:match('<input type="hidden" name="(.-)" value="(.-)">')
--                 args[k] = v
--             end
--             googlev = args.v
--             writefile('googlev.txt', args.v)
--         end
    
--         local function got(url, Method, Body) -- Basic version of https://www.npmjs.com/package/got using synapse's request API for google websites
--             Method = Method or "GET"
            
--             local res = request({
--                 Url = url,
--                 Method = Method,
--                 Headers = {cookie="CONSENT=YES+"..googlev},
--                 Body = Body
--             })
            
--             if res.Body:match('https://consent.google.com/s') then
--                 googleConsent(res.Body)
--                 res = request({
--                     Url = url,
--                     Method = "GET",
--                     Headers = {cookie="CONSENT=YES+"..googlev}
--                 })
--             end
            
--             return res
--         end
    
--         getgenv().languages = {
--             auto = "Automatic",
--             ['zh-cn'] = "Chinese Simplified",
--             ['zh-tw'] = "Chinese Traditional",
--             en = "English",
--             fr = "French",
--             de = "German",
--             el = "Greek",
--             hu = "Hungarian",
--             id = "Indonesian",
--             it = "Italian",
--             ja = "Japanese",
--             ko = "Korean",
--             mg = "Malagasy",
--             pl = "Polish",
--             pt = "Portuguese",
--             ru = "Russian",
--             es = "Spanish",
--             tr = "Turkish",
--             vi = "Vietnamese",
--         };
--         local listl = {}
--         for k,v in pairs(languages) do table.insert(listl,k) end
--         function SetRandomLang() 
--             YourLang = listl[math.random(1,#listl)]
--         end
--         function find(lang)
--             for i,v in pairs(languages) do
--                 if i == lang or v == lang then
--                     return i
--                 end
--             end
--         end
    
--         function isSupported(lang)
--             local key = find(lang)
--             return key and true or false 
--         end
    
--         function getISOCode(lang)
--             local key = find(lang)
--             return key
--         end
    
--         function stringifyQuery(dataFields)
--             local data = ""
--             for k, v in pairs(dataFields) do
--                 if type(v) == "table" then
--                     for _,v in pairs(v) do
--                         data = data .. ("&%s=%s"):format(
--                             game.HttpService:UrlEncode(k),
--                             game.HttpService:UrlEncode(v)
--                         )
--                     end
--                 else
--                     data = data .. ("&%s=%s"):format(
--                         game.HttpService:UrlEncode(k),
--                         game.HttpService:UrlEncode(v)
--                     )
--                 end
--             end
--             data = data:sub(2)
--             return data
--         end
    
--         local reqid = math.random(1000,9999)
--         local rpcidsTranslate = "MkEWBc"
--         local rootURL = "https://translate.google.com/"
--         local executeURL = "https://translate.google.com/_/TranslateWebserverUi/data/batchexecute"
--         local fsid, bl
    
--         do -- init
--             local InitialReq = got(rootURL)
--             fsid = InitialReq.Body:match('"FdrFJe":"(.-)"')
--             bl = InitialReq.Body:match('"cfb2h":"(.-)"')
--         end
    
--         local HttpService = game:GetService("HttpService")
--         function jsonE(o)
--             return HttpService:JSONEncode(o)
--         end
--         function jsonD(o)
--             return HttpService:JSONDecode(o)
--         end
    
--         function translate(str, to, from)
--             reqid = reqid + 10000
--             from = from and getISOCode(from) or 'auto'
--             to = to and getISOCode(to) or 'en'
    
--             local data = {{str, from, to, true}, {nil}}
    
--             local freq = {
--                 {
--                     {
--                         rpcidsTranslate, 
--                         jsonE(data),
--                         nil,
--                         "generic"
--                     }
--                 }
--             }
    
--             local url = executeURL..'?'..stringifyQuery{rpcids = rpcidsTranslate, ['f.sid'] = fsid, bl = bl, hl="en", _reqid = reqid-10000, rt = 'c'}
--             local body = stringifyQuery{['f.req'] = jsonE(freq)}
            
--             local req = got(url, "POST", body)
            
--             local body = jsonD(req.Body:match'%[.-%]\n')
--             local translationData = jsonD(body[1][3])
--             local result = {
--                 text = "",
--                 from = {
--                     language = "",
--                     text = ""
--                 },
--                 raw = ""
--             }
--             result.raw = translationData
--             result.text = translationData[2][1][1][6][1][1]
            
--             result.from.language = translationData[3]
--             result.from.text = translationData[2][5][1]
    
--             return result
--         end
--     end
--     function translateFrom(message)
--         local translation = translate(message, YourLang)
    
--         local text
--         if translation.from.language ~= YourLang then 
--             text = translation.text
--         end
    
--         return {text, translation.from.language}
--     end
--     function Translate(message) 
--         local s,translated =  pcall(function() 
--             return translateFrom(message)[1]
--         end)
--         if s then return translated 
--         else
--             --print(message,translated)
--         end
--     end
-- end
-- SetUpTranslate()
-- getgenv().TranslateCache = {}
-- if not isfolder("Sea Hub") then
--     makefolder("Sea Hub")
-- end
-- local s,Translated = pcall(function() 
--     return game.HttpService:JSONDecode(readfile("Sea Hub/!UIText.json"))
-- end)
-- function SaveFile() 
--     pcall(function() 
--         writefile("Sea Hub/!UIText.json",game.HttpService:JSONEncode(getgenv().TranslateCache))
--     end)
-- end
-- function isnumber() end
-- local UIChanged = false
-- if s and Translated then 
--     getgenv().TranslateCache = Translated end
-- if GUI then 
--     GUI.DescendantAdded:Connect(function(des) 
--         if des then 
--             if pcall(function() return des.Text end) then 
--                 delay(0,function() 
--                     if des.Text=="" or #des.Text<=4 or tonumber(des.Text)~=nil then
--                         return
--                     end
--                     if string.match(des.Text,"Sea Hub") then 
--                         local tvk = des.Text:gsub("Sea Hub","Trung Tâm Biển")
--                         des.Text = tvk
--                         return
--                     end
--                     local old = des.Text
--                     local c = 0
--                     while des.Text==old and c<3 do 
--                         --SetRandomLang()
--                         if getgenv().TranslateCache[des.Text] then 
--                             des.Text = getgenv().TranslateCache[des.Text]
--                             return
--                         end
--                         local t = Translate(des.Text)
--                         if t and t ~= old then 
--                             getgenv().TranslateCache[des.Text] = t
--                             UIChanged =true
--                             if t then des.Text = t end
--                         end
--                         wait(1)
--                         c=c+1
--                     end
--                     getgenv().TranslateCache[des.Text]  = des.Text
--                     UIChanged =true
--                 end)
--             end
--         end
--     end)
-- end
-- spawn(function() 
--     local t = tick()
--     while wait(2) do 
--         if tick()-t>30 then 
--             if UIChanged then 
--                 SaveFile()
--                 UIChanged = false
--             end
--         else
--             SaveFile()
--         end
--     end
-- end)
-- if syn.protect_gui then
--     syn.protect_gui(u.Gui)
--     syn.protect_gui(u.NotiGui)
--     u.Gui.Parent = game:GetService("CoreGui")
--     u.NotiGui.Parent = game:GetService("CoreGui")
-- end
u.Gui.Parent = game:GetService("CoreGui")
u.NotiGui.Parent = game:GetService("CoreGui")

function u.Getcolor(g)
    return {math.floor(g.r * 255), math.floor(g.g * 255), math.floor(g.b * 255)}
end
function t.CreateNoti(H)
    getgenv().TitleNameNoti = H.Title or ""
    local I = H.Desc
    local J = H.ShowTime or 10
    local K = Instance.new("Frame")
    local L = Instance.new("Frame")
    local M = Instance.new("UICorner")
    local N = Instance.new("Frame")
    local O = Instance.new("ImageLabel")
    local P = Instance.new("UICorner")
    local Q = Instance.new("TextLabel")
    local R = Instance.new("Frame")
    local S = Instance.new("ImageLabel")
    local T = Instance.new("TextButton")
    local U = Instance.new("TextLabel")
    K.Name = "NotiFrame"
    K.Parent = F
    K.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    K.BackgroundTransparency = 1.000
    K.ClipsDescendants = true
    K.Position = UDim2.new(0, 0, 0, 0)
    K.Size = UDim2.new(1, 0, 0, 0)
    K.AutomaticSize = Enum.AutomaticSize.Y
    L.Name = "Noticontainer"
    L.Parent = K
    L.Position = UDim2.new(1, 0, 0, 0)
    L.Size = UDim2.new(1, 0, 1, 6)
    L.AutomaticSize = Enum.AutomaticSize.Y
    L.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
    table.insert(
        c["Background 3 Color"],
        function()
            L.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
        end
    )
    M.CornerRadius = UDim.new(0, 4)
    M.Parent = L
    N.Name = "Topnoti"
    N.Parent = L
    N.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    N.BackgroundTransparency = 1.000
    N.Position = UDim2.new(0, 0, 0, 5)
    N.Size = UDim2.new(1, 0, 0, 25)
    O.Name = "Ruafimg"
    O.Parent = N
    O.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    O.BackgroundTransparency = 1.000
    O.Position = UDim2.new(0, 10, 0, 0)
    O.Size = UDim2.new(0, 25, 0, 25)
    O.Image = getgenv().UIColor["Logo Image"]
    table.insert(
        c["Logo Image"],
        function()
            O.Image = u.GetIMG(getgenv().UIColor["Logo Image"])
        end
    )
    P.CornerRadius = UDim.new(1, 0)
    P.Name = "RuafimgCorner"
    P.Parent = O
    local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
    local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
    local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
    local g = V .. "," .. W .. "," .. X
    Q.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().TitleNameNoti
    table.insert(
        c["Title Text Color"],
        function()
            local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
            local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
            local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
            local g = V .. "," .. W .. "," .. X
            Q.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().TitleNameNoti
        end
    )
    Q.Name = "TextLabelNoti"
    Q.Parent = N
    Q.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    Q.BackgroundTransparency = 1.000
    Q.Position = UDim2.new(0, 40, 0, 0)
    Q.Size = UDim2.new(1, -40, 1, 0)
    Q.Font = Enum.Font.GothamBold
    Q.TextSize = 14.000
    Q.TextWrapped = true
    Q.TextXAlignment = Enum.TextXAlignment.Left
    Q.RichText = true
    Q.TextColor3 = getgenv().UIColor["GUI Text Color"]
    table.insert(
        c["GUI Text Color"],
        function()
            Q.TextColor3 = getgenv().UIColor["GUI Text Color"]
        end
    )
    R.Name = "CloseContainer"
    R.Parent = N
    R.AnchorPoint = Vector2.new(1, 0.5)
    R.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    R.BackgroundTransparency = 1.000
    R.Position = UDim2.new(1, -4, 0.5, 0)
    R.Size = UDim2.new(0, 22, 0, 22)
    S.Name = "CloseImage"
    S.Parent = R
    S.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    S.BackgroundTransparency = 1.000
    S.Size = UDim2.new(1, 0, 1, 0)
    S.Image = "rbxassetid://3926305904"
    S.ImageRectOffset = Vector2.new(284, 4)
    S.ImageRectSize = Vector2.new(24, 24)
    S.ImageColor3 = getgenv().UIColor["Search Icon Color"]
    table.insert(
        c["Search Icon Color"],
        function()
            S.ImageColor3 = getgenv().UIColor["Search Icon Color"]
        end
    )
    T.Parent = R
    T.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    T.BackgroundTransparency = 1.000
    T.Size = UDim2.new(1, 0, 1, 0)
    T.Font = Enum.Font.SourceSans
    T.Text = ""
    T.TextColor3 = Color3.fromRGB(0, 0, 0)
    T.TextSize = 14.000
    if I then
        U.Name = "TextColor"
        U.Parent = L
        U.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        U.BackgroundTransparency = 1.000
        U.Position = UDim2.new(0, 10, 0, 35)
        U.Size = UDim2.new(1, -15, 0, 0)
        U.Font = Enum.Font.GothamBold
        U.Text = I
        U.TextSize = 14.000
        U.TextXAlignment = Enum.TextXAlignment.Left
        U.RichText = true
        U.TextColor3 = getgenv().UIColor["Text Color"]
        U.AutomaticSize = Enum.AutomaticSize.Y
        U.TextWrapped = true
        table.insert(
            c["Text Color"],
            function()
                U.TextColor3 = getgenv().UIColor["Text Color"]
            end
        )
    end
    local function Y()
        w:Create(L, TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]), {Position = UDim2.new(1, 0, 0, 0)}):Play(

        )
        wait(.25)
        K:Destroy()
    end
    w:Create(L, TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]), {Position = UDim2.new(0, 0, 0, 0)}):Play()
    T.MouseEnter:Connect(
        function()
            w:Create(
                S,
                TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                {ImageColor3 = getgenv().UIColor["Search Icon Highlight Color"]}
            ):Play()
        end
    )
    T.MouseLeave:Connect(
        function()
            w:Create(
                S,
                TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                {ImageColor3 = getgenv().UIColor["Search Icon Color"]}
            ):Play()
        end
    )
    T.MouseButton1Click:Connect(
        function()
            spawn(
                function()
                    u.ButtonEffect()
                end
            )
            wait(.25)
            Y()
        end
    )
    spawn(
        function()
            wait(J)
            Y()
        end
    )
end
function t.CreateMain(H)
    local Z = tostring(H.Title) or "Sea Hub"
    getgenv().MainDesc = H.Desc or ""
    local _ = false
    cac = false
    local function a0(a1, a2)
        local a3 = nil
        local a4 = nil
        local a5 = nil
        local a6 = nil
        a1.InputBegan:Connect(
            function(a7)
                if a7.UserInputType == Enum.UserInputType.MouseButton1 or a7.UserInputType == Enum.UserInputType.Touch then
                    a3 = true
                    a5 = a7.Position
                    a6 = a2.Position
                    a7.Changed:Connect(
                        function()
                            if a7.UserInputState == Enum.UserInputState.End then
                                a3 = false
                            end
                        end
                    )
                end
            end
        )
        a1.InputChanged:Connect(
            function(a7)
                if a7.UserInputType == Enum.UserInputType.MouseMovement or a7.UserInputType == Enum.UserInputType.Touch then
                    a4 = a7
                end
            end
        )
        x.InputChanged:Connect(
            function(a7)
                if a7 == a4 and a3 then
                    local a8 = a7.Position - a5
                    if not _ and cac then
                        w:Create(
                            a2,
                            TweenInfo.new(0.35, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
                            {Position = UDim2.new(a6.X.Scale, a6.X.Offset + a8.X, a6.Y.Scale, a6.Y.Offset + a8.Y)}
                        ):Play()
                    elseif not _ and not cac then
                        a2.Position = UDim2.new(a6.X.Scale, a6.X.Offset + a8.X, a6.Y.Scale, a6.Y.Offset + a8.Y)
                    end
                end
            end
        )
    end
    local a9 = Instance.new("Frame")
    local aa = Instance.new("ImageLabel")
    local ab = Instance.new("UICorner")
    local ac = Instance.new("Frame")
    local O = Instance.new("ImageLabel")
    local ad = Instance.new("TextLabel")
    local ae = Instance.new("Frame")
    local M = Instance.new("UICorner")
    local af = Instance.new("ScrollingFrame")
    local ag = Instance.new("UIListLayout")
    local ah = Instance.new("TextLabel")
    local ai = Instance.new("Frame")
    local aj = Instance.new("UIPageLayout")
    local ak = Instance.new("Frame")
    local al = Instance.new("TextButton")
    local am = Instance.new("ImageLabel")
    local an = Instance.new("Frame")
    local ao = Instance.new("Frame")
    local ap = Instance.new("Frame")
    local aq = Instance.new("UIPageLayout")
    local ar
    a9.Name = "Main"
    a9.Parent = u.Gui
    a9.BackgroundColor3 = Color3.fromRGB(42, 42, 42)
    a9.BackgroundTransparency = 1.000
    a9.Position = UDim2.new(0.5, 0, 0.5, 0)
    a9.AnchorPoint = Vector2.new(0.5, 0.5)
    a9.Size = UDim2.new(0, 629, 0, 359)
    a0(a9, a9)
    aa.Name = "maingui"
    aa.Parent = a9
    aa.AnchorPoint = Vector2.new(0.5, 0.5)
    aa.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    aa.BackgroundTransparency = 1.000
    aa.Position = UDim2.new(0.5, 0, 0.5, 0)
    aa.Selectable = true
    aa.Size = UDim2.new(1, 30, 1, 30)
    aa.Image = "rbxassetid://8068653048"
    aa.ScaleType = Enum.ScaleType.Slice
    aa.SliceCenter = Rect.new(15, 15, 175, 175)
    aa.SliceScale = 1.300
    aa.ImageColor3 = getgenv().UIColor["Border Color"]
    table.insert(
        c["Border Color"],
        function()
            aa.ImageColor3 = getgenv().UIColor["Border Color"]
        end
    )
    function u.ReloadMain(v)
        aa.ImageColor3 = getgenv().UIColor["Title Text Color"]
        local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
        local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
        local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
        local g = V .. "," .. W .. "," .. X
        ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
        table.insert(
            c["Title Text Color"],
            function()
                aa.ImageColor3 = getgenv().UIColor["Title Text Color"]
                local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
                local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
                local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
                local g = V .. "," .. W .. "," .. X
                ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
            end
        )
        local as
        if
            v ~= "" and type(v) == "string" and string.find(v:lower(), ".webm") and
                pcall(
                    function()
                        writefile("seahub.webm", syn.request({Url = v}).Body)
                    end
                )
         then
            wait(.25)
            local at = isfile("seahub.webm")
            wait(.25)
            if at then
                as = Instance.new("VideoFrame")
                as.Name = "MainContainer"
                as.Parent = a9
                as.BackgroundColor3 = getgenv().UIColor["Background Main Color"]
                as.Size = UDim2.new(1, 0, 1, 0)
                as.Video = getsynasset("seahub.webm")
                as.Looped = true
                as:Play()
                wait(.5)
                delfile("seahub.webm")
            end
        else
            as = Instance.new("ImageLabel")
            as.Name = "MainContainer"
            as.Parent = a9
            as.BackgroundColor3 = getgenv().UIColor["Background Main Color"]
            as.Size = UDim2.new(1, 0, 1, 0)
            as.Image = u.GetIMG(v)
        end
        MainCorner_ = Instance.new("UICorner")
        MainCorner_.CornerRadius = UDim.new(0, 4)
        MainCorner_.Name = "MainCorner"
        MainCorner_.Parent = as
        for a, m in next, a9:GetChildren() do
            if m.Name == "MainContainer" then
                for a, v in next, m:GetChildren() do
                    v.Parent = as
                end
                wait()
                m:Destroy()
                break
            end
        end
        table.insert(
            c["Background 3 Color"],
            function()
                as.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
            end
        )
    end
    aa.ImageColor3 = getgenv().UIColor["Title Text Color"]
    local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
    local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
    local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
    local g = V .. "," .. W .. "," .. X
    ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
    table.insert(
        c["Title Text Color"],
        function()
            aa.ImageColor3 = getgenv().UIColor["Title Text Color"]
            local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
            local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
            local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
            local g = V .. "," .. W .. "," .. X
            ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
        end
    )
    local ar
    local au = getgenv().UIColor["Background Image"]
    if
        au ~= "" and type(au) == "string" and string.find(au:lower(), ".webm") and
            pcall(
                function()
                    writefile("seahub.webm", syn.request({Url = au}).Body)
                end
            )
     then
        wait(.25)
        local at = isfile("seahub.webm")
        wait(.25)
        if at then
            ar = Instance.new("VideoFrame")
            ar.Name = "MainContainer"
            ar.Parent = a9
            ar.BackgroundColor3 = getgenv().UIColor["Background Main Color"]
            ar.Size = UDim2.new(1, 0, 1, 0)
            ar.Video = getsynasset("seahub.webm")
            ar.Looped = true
            ar:Play()
            wait(.5)
            delfile("seahub.webm")
        end
    else
        ar = Instance.new("ImageLabel")
        ar.Name = "MainContainer"
        ar.Parent = a9
        ar.BackgroundColor3 = getgenv().UIColor["Background Main Color"]
        ar.Size = UDim2.new(1, 0, 1, 0)
        ar.Image = u.GetIMG(au)
    end
    table.insert(
        c["Background 3 Color"],
        function()
            ar.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
        end
    )
    getgenv().ReadyForGuiLoaded = true
    ab.CornerRadius = UDim.new(0, 4)
    ab.Name = "MainCorner"
    ab.Parent = ar
    an.Name = "Concacontainer"
    an.Parent = ar
    an.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    an.BackgroundTransparency = 1.000
    an.ClipsDescendants = true
    an.Position = UDim2.new(0, 0, 0, 30)
    an.Size = UDim2.new(1, 0, 1, -30)
    ao.Name = "Concacmain"
    ao.Parent = an
    ao.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ao.BackgroundTransparency = 1.000
    ao.Selectable = true
    ao.Size = UDim2.new(1, 0, 1, 0)
    ap.Name = "Background1"
    ap.Parent = an
    ap.LayoutOrder = 1
    ap.Selectable = true
    ap.Size = UDim2.new(1, 0, 1, 0)
    ap.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
    table.insert(
        c["Background 1 Transparency"],
        function()
            ap.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
        end
    )
    ap.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
    table.insert(
        c["Background 1 Color"],
        function()
            ap.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
        end
    )
    aq.Name = "Concacpage"
    aq.Parent = an
    aq.SortOrder = Enum.SortOrder.LayoutOrder
    aq.EasingDirection = Enum.EasingDirection.InOut
    aq.EasingStyle = Enum.EasingStyle.Quad
    aq.TweenTime = getgenv().UIColor["Tween Animation 1 Speed"]
    table.insert(
        c["Tween Animation 1 Speed"],
        function()
            aq.TweenTime = getgenv().UIColor["Tween Animation 1 Speed"]
        end
    )
    ac.Name = "TopMain"
    ac.Parent = ar
    ac.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ac.BackgroundTransparency = 1.000
    ac.Size = UDim2.new(1, 0, 0, 25)
    O.Name = "Ruafimg"
    O.Parent = ac
    O.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    O.BackgroundTransparency = 1.000
    O.Position = UDim2.new(0, 5, 0, 0)
    O.Size = UDim2.new(0, 25, 0, 25)
    O.Image = getgenv().UIColor["Logo Image"]
    table.insert(
        c["Logo Image"],
        function()
            O.Image = getgenv().UIColor["Logo Image"]
        end
    )
    ad.Name = "TextLabelMain"
    ad.Parent = ac
    ad.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    ad.BackgroundTransparency = 1.000
    ad.Position = UDim2.new(0, 35, 0, 0)
    ad.Size = UDim2.new(1, -35, 1, 0)
    ad.Font = Enum.Font.GothamBold
    ad.RichText = true
    ad.TextSize = 16.000
    ad.TextWrapped = true
    ad.TextXAlignment = Enum.TextXAlignment.Left
    ad.TextColor3 = getgenv().UIColor["GUI Text Color"]
    table.insert(
        c["GUI Text Color"],
        function()
            ad.TextColor3 = getgenv().UIColor["GUI Text Color"]
        end
    )
    local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
    local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
    local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
    local g = V .. "," .. W .. "," .. X
    ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
    table.insert(
        c["Title Text Color"],
        function()
            local V = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[1])
            local W = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[2])
            local X = tostring(u.Getcolor(getgenv().UIColor["Title Text Color"])[3])
            local g = V .. "," .. W .. "," .. X
            ad.Text = '<font color="rgb(' .. g .. ')">Sea Hub</font> ' .. getgenv().MainDesc
        end
    )
    ak.Name = "SettionMain"
    ak.Parent = ac
    ak.AnchorPoint = Vector2.new(1, 0)
    ak.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ak.BackgroundTransparency = 1.000
    ak.Position = UDim2.new(1, 0, 0, 0)
    ak.Size = UDim2.new(0, 30, 0, 30)
    al.Name = "SettionButton"
    al.Parent = ak
    al.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    al.BackgroundTransparency = 1.000
    al.BorderColor3 = Color3.fromRGB(27, 42, 53)
    al.Size = UDim2.new(1, 0, 1, 0)
    al.Font = Enum.Font.SourceSans
    al.Text = ""
    al.TextColor3 = Color3.fromRGB(0, 0, 0)
    al.TextSize = 14.000
    al.Visible = true
    am.Name = "SettingIcon"
    am.Parent = ak
    am.AnchorPoint = Vector2.new(0.5, 0.5)
    am.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    am.BackgroundTransparency = 1.000
    am.Position = UDim2.new(0.5, 0, 0.5, 0)
    am.Size = UDim2.new(1, -10, 1, -10)
    am.Image = "rbxassetid://7397332215"
    am.Visible = true
    am.ImageColor3 = getgenv().UIColor["Setting Icon Color"]
    table.insert(
        c["Setting Icon Color"],
        function()
            am.ImageColor3 = getgenv().UIColor["Setting Icon Color"]
        end
    )
    ae.Name = "Background1"
    ae.Parent = ao
    ae.Position = UDim2.new(0, 5, 0, 0)
    ae.Size = UDim2.new(0, 180, 0, 325)
    ae.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
    table.insert(
        c["Background 1 Transparency"],
        function()
            ae.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
        end
    )
    ae.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
    table.insert(
        c["Background 1 Color"],
        function()
            ae.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
        end
    )
    M.CornerRadius = UDim.new(0, 4)
    M.Parent = ae
    af.Name = "ControlList"
    af.Parent = ae
    af.Active = true
    af.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    af.BackgroundTransparency = 1.000
    af.BorderColor3 = Color3.fromRGB(27, 42, 53)
    af.BorderSizePixel = 0
    af.Position = UDim2.new(0, 0, 0, 30)
    af.Size = UDim2.new(1, -5, 1, -30)
    af.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
    af.CanvasSize = UDim2.new(0, 0, 0, 0)
    af.ScrollBarThickness = 5
    af.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
    ag.Parent = af
    ag.SortOrder = Enum.SortOrder.LayoutOrder
    ag.Padding = UDim.new(0, 5)
    ah.Name = "GUITextColor"
    ah.Parent = ae
    ah.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    ah.BackgroundTransparency = 1.000
    ah.Position = UDim2.new(0, 5, 0, 0)
    ah.Size = UDim2.new(1, 0, 0, 25)
    ah.Font = Enum.Font.GothamBold
    ah.Text = Z
    ah.TextSize = 14.000
    ah.TextXAlignment = Enum.TextXAlignment.Left
    ah.TextColor3 = getgenv().UIColor["GUI Text Color"]
    table.insert(
        c["GUI Text Color"],
        function()
            ah.TextColor3 = getgenv().UIColor["GUI Text Color"]
        end
    )
    ai.Name = "MainPage"
    ai.Parent = ao
    ai.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    ai.BackgroundTransparency = 1.000
    ai.ClipsDescendants = true
    ai.Position = UDim2.new(0, 190, 0, 0)
    ai.Size = UDim2.new(0, 435, 0, 325)
    aj.Name = "UIPage"
    aj.Parent = ai
    aj.FillDirection = Enum.FillDirection.Vertical
    aj.SortOrder = Enum.SortOrder.LayoutOrder
    aj.EasingDirection = Enum.EasingDirection.InOut
    aj.EasingStyle = Enum.EasingStyle.Quart
    aj.Padding = UDim.new(0, 10)
    aj.TweenTime = getgenv().UIColor["Tween Animation 1 Speed"]
    aj.ScrollWheelInputEnabled = false
    table.insert(
        c["Tween Animation 1 Speed"],
        function()
            aj.TweenTime = getgenv().UIColor["Tween Animation 1 Speed"]
        end
    )
    ag:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
        function()
            af.CanvasSize = UDim2.new(0, 0, 0, ag.AbsoluteContentSize.Y + 5)
        end
    )
    local av = false
    al.MouseButton1Click:Connect(
        function()
            u.ButtonEffect()
        end
    )
    al.MouseButton1Click:Connect(
        function()
            av = not av
            pa = av and 1 or 0
            ro = av and 180 or 0
          --  aq:JumpToIndex(pa)
            game.TweenService:Create(am, TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]), {Rotation = ro}):Play(

            )
        end
    )
    local aw = Instance.new("ScrollingFrame")
    local ax = Instance.new("UIListLayout")
    aw.Name = "CustomList"
    aw.Parent = ap
    aw.Active = true
    aw.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    aw.BackgroundTransparency = 1.000
    aw.BorderColor3 = Color3.fromRGB(27, 42, 53)
    aw.BorderSizePixel = 0
    aw.Position = UDim2.new(0, 5, 0, 30)
    aw.Size = UDim2.new(1, -10, 1, -30)
    aw.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
    aw.ScrollBarThickness = 5
    aw.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
    ax.Name = "CustomListLayout"
    ax.Parent = aw
    ax.SortOrder = Enum.SortOrder.LayoutOrder
    ax.Padding = UDim.new(0, 5)
    ax:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
        function()
            aw.CanvasSize = UDim2.new(0, 0, 0, ax.AbsoluteContentSize.Y + 5)
        end
    )
    local ay = Instance.new("TextLabel")
    ay.Name = "GUITextColor"
    ay.Parent = ap
    ay.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ay.BackgroundTransparency = 1.000
    ay.Position = UDim2.new(0, 15, 0, 0)
    ay.Size = UDim2.new(1, -15, 0, 25)
    ay.Font = Enum.Font.GothamBold
    ay.Text = ""
    ay.TextSize = 16.000
    ay.TextXAlignment = Enum.TextXAlignment.Left
    ay.TextColor3 = getgenv().UIColor["GUI Text Color"]
    table.insert(
        c["GUI Text Color"],
        function()
            ay.TextColor3 = getgenv().UIColor["GUI Text Color"]
        end
    )
    local az = Instance.new("Frame")
    local aA = Instance.new("UICorner")
    local aB = Instance.new("Frame")
    local aC = Instance.new("ImageLabel")
    local aD = Instance.new("TextButton")
    local aE = Instance.new("TextBox")
    az.Name = "Background2"
    az.Parent = ap
    az.AnchorPoint = Vector2.new(1, 0)
    az.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
    az.ClipsDescendants = true
    az.Position = UDim2.new(1, -5, 0, 5)
    az.Size = UDim2.new(0, 20, 0, 20)
    az.ClipsDescendants = true
    table.insert(
        c["Background 2 Color"],
        function()
            az.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
        end
    )
    aA.CornerRadius = UDim.new(0, 2)
    aA.Name = "PageSearchCorner"
    aA.Parent = az
    aB.Name = "SearchFrame"
    aB.Parent = az
    aB.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    aB.BackgroundTransparency = 1.000
    aB.Size = UDim2.new(0, 20, 0, 20)
    aC.Name = "SearchIcon"
    aC.Parent = aB
    aC.AnchorPoint = Vector2.new(0.5, 0.5)
    aC.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    aC.BackgroundTransparency = 1.000
    aC.Position = UDim2.new(0.5, 0, 0.5, 0)
    aC.Size = UDim2.new(0, 16, 0, 16)
    aC.Image = "rbxassetid://8154282545"
    aC.ImageColor3 = getgenv().UIColor["Search Icon Color"]
    table.insert(
        c["Search Icon Color"],
        function()
            aC.ImageColor3 = getgenv().UIColor["Search Icon Color"]
        end
    )
    aD.Name = "active"
    aD.Parent = aB
    aD.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    aD.BackgroundTransparency = 1.000
    aD.Size = UDim2.new(1, 0, 1, 0)
    aD.Font = Enum.Font.SourceSans
    aD.Text = ""
    aD.TextColor3 = Color3.fromRGB(0, 0, 0)
    aD.TextSize = 14.000
    aE.Name = "TextColorPlaceholder"
    aE.Parent = az
    aE.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    aE.BackgroundTransparency = 1.000
    aE.Position = UDim2.new(0, 30, 0, 0)
    aE.Size = UDim2.new(1, -30, 1, 0)
    aE.Font = Enum.Font.GothamBold
    aE.Text = ""
    aE.TextSize = 14.000
    aE.TextXAlignment = Enum.TextXAlignment.Left
    aE.PlaceholderText = "Search Section name"
    aE.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
    aE.TextColor3 = getgenv().UIColor["Text Color"]
    table.insert(
        c["Placeholder Text Color"],
        function()
            aE.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
        end
    )
    table.insert(
        c["Text Color"],
        function()
            aE.TextColor3 = getgenv().UIColor["Text Color"]
        end
    )
    local aF = false
    aD.MouseEnter:Connect(
        function()
            w:Create(
                aC,
                TweenInfo.new(getgenv().UIColor["Tween Animation 3 Speed"]),
                {ImageColor3 = getgenv().UIColor["Search Icon Highlight Color"]}
            ):Play()
        end
    )
    aD.MouseLeave:Connect(
        function()
            w:Create(
                aC,
                TweenInfo.new(getgenv().UIColor["Tween Animation 3 Speed"]),
                {ImageColor3 = getgenv().UIColor["Search Icon Color"]}
            ):Play()
        end
    )
    aD.MouseButton1Click:Connect(
        function()
            u.ButtonEffect()
        end
    )
    aE.Focused:Connect(
        function()
            u.ButtonEffect()
        end
    )
    aD.MouseButton1Click:Connect(
        function()
            aF = not aF
            local aG = aF and UDim2.new(0, 175, 0, 20) or UDim2.new(0, 20, 0, 20)
            game.TweenService:Create(az, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = aG}):Play(

            )
        end
    )
    local function aH()
        for a, v in next, aw:GetChildren() do
            if not v:IsA("UIListLayout") then
                v.Visible = false
            end
        end
    end
    local function aI()
        for n, B in pairs(aw:GetChildren()) do
            if not B:IsA("UIListLayout") then
                if string.find(string.lower(B.Name), string.lower(aE.Text)) then
                    B.Visible = true
                end
            end
        end
    end
    aE:GetPropertyChangedSignal("Text"):Connect(
        function()
            aH()
            aI()
        end
    )
    function t.CreateCustomColor(aJ)
        ay.Text = aJ or "Custom GUI"
        local aK = {}
        function aK.CreateSection(aL)
            local aM = Instance.new("Frame")
            local M = Instance.new("UICorner")
            local aN = Instance.new("Frame")
            local aO = Instance.new("TextLabel")
            local aP = Instance.new("Frame")
            local aQ = Instance.new("UIGradient")
            local aR = Instance.new("UIListLayout")
            local aS = aL or "Section"
            aM.Name = aL .. "Section"
            aM.Parent = aw
            aM.Size = UDim2.new(1, 0, 0, 285)
            aM.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
            table.insert(
                c["Background 3 Color"],
                function()
                    aM.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
                end
            )
            aM.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
            table.insert(
                c["Background 1 Transparency"],
                function()
                    aM.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                end
            )
            M.CornerRadius = UDim.new(0, 4)
            M.Parent = aM
            aN.Name = "Topsec"
            aN.Parent = aM
            aN.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            aN.BackgroundTransparency = 1.000
            aN.Size = UDim2.new(1, 0, 0, 27)
            aO.Name = "Sectiontitle"
            aO.Parent = aN
            aO.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            aO.BackgroundTransparency = 1.000
            aO.Size = UDim2.new(1, 0, 1, 0)
            aO.Font = Enum.Font.GothamBold
            aO.Text = aL
            aO.TextSize = 14.000
            aO.TextColor3 = getgenv().UIColor["Section Text Color"]
            table.insert(
                c["Section Text Color"],
                function()
                    aO.TextColor3 = getgenv().UIColor["Section Text Color"]
                end
            )
            aP.Name = "Linesec"
            aP.Parent = aN
            aP.AnchorPoint = Vector2.new(0.5, 1)
            aP.BorderSizePixel = 0
            aP.Position = UDim2.new(0.5, 0, 1, -2)
            aP.Size = UDim2.new(1, -10, 0, 2)
            aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
            table.insert(
                c["Section Underline Color"],
                function()
                    aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
                end
            )
            aQ.Transparency =
                NumberSequence.new {
                NumberSequenceKeypoint.new(0.00, 1.00),
                NumberSequenceKeypoint.new(0.50, 0.00),
                NumberSequenceKeypoint.new(0.51, 0.02),
                NumberSequenceKeypoint.new(1.00, 1.00)
            }
            aQ.Parent = aP
            aR.Name = "SectionList"
            aR.Parent = aM
            aR.SortOrder = Enum.SortOrder.LayoutOrder
            aR.Padding = UDim.new(0, 5)
            aR:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
                function()
                    aM.Size = UDim2.new(1, 0, 0, aR.AbsoluteContentSize.Y + 5)
                end
            )
            local aT = {}
            function aT.CreateColorPicker(H)
                local aU =
                    setmetatable(
                    {},
                    {__index = function(p, q)
                            if q == "Cungroi" then
                                return e[H.Type].Rainbow
                            end
                        end, __newindex = function(p, q, r)
                            if q == "Cungroi" then
                                e[H.Type].Rainbow = r
                            end
                        end}
                )
                local aV, aW, aX
                local aY = H.Title or "Color Picker"
                local aZ = e[H.Type].Color or Color3.fromRGB(255, 255, 255)
                local a_ = H.Type
                local b0 = Instance.new("Frame")
                local b1 = Instance.new("UICorner")
                local b2 = Instance.new("Frame")
                local b3 = Instance.new("UICorner")
                local b4 = Instance.new("TextLabel")
                local b5 = Instance.new("Frame")
                local b6 = Instance.new("UICorner")
                local b7 = Instance.new("TextButton")
                local b8 = Instance.new("Frame")
                local b9 = Instance.new("UIGradient")
                local ba = Instance.new("Frame")
                local M = Instance.new("UICorner")
                local bb = Instance.new("Frame")
                local bc = Instance.new("Frame")
                local bd = Instance.new("TextLabel")
                local be = Instance.new("TextBox")
                local bf = Instance.new("Frame")
                local bg = Instance.new("TextLabel")
                local bh = Instance.new("TextBox")
                local bi = Instance.new("Frame")
                local bj = Instance.new("TextLabel")
                local bk = Instance.new("TextBox")
                local ag = Instance.new("UIListLayout")
                local bl = Instance.new("Frame")
                local bm = Instance.new("TextLabel")
                local bn = Instance.new("TextBox")
                local aP = Instance.new("Frame")
                local aQ = Instance.new("UIGradient")
                local bo = Instance.new("Frame")
                local bp = Instance.new("Frame")
                local bq = Instance.new("TextLabel")
                local br = Instance.new("ImageLabel")
                local bs = Instance.new("ImageLabel")
                local bt = Instance.new("TextButton")
                local bu = Instance.new("ImageLabel")
                local bv = Instance.new("Frame")
                local bw = Instance.new("UICorner")
                local bx = Instance.new("Frame")
                local by = Instance.new("Frame")
                local bz = Instance.new("TextLabel")
                local bA = Instance.new("ImageLabel")
                local bB = Instance.new("ImageLabel")
                local bC = Instance.new("TextButton")
                local bD = Instance.new("Frame")
                local bE = Instance.new("UIListLayout")
                local bF = Instance.new("Frame")
                local bG = Instance.new("UICorner")
                local bH = Instance.new("TextButton")
                local bI = Instance.new("Frame")
                local bJ = Instance.new("UICorner")
                local bK = Instance.new("TextButton")
                b0.Name = "ColorPick"
                b0.Parent = aM
                b0.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                b0.BackgroundTransparency = 1.000
                b0.ClipsDescendants = true
                b0.Position = UDim2.new(0, 0, 0.112280704, 0)
                b0.Size = UDim2.new(1, 0, 0, 35)
                b1.CornerRadius = UDim.new(0, 4)
                b1.Name = "ColorPickCorner"
                b1.Parent = b0
                b2.Name = "Background1"
                b2.Parent = b0
                b2.AnchorPoint = Vector2.new(0.5, 0.5)
                b2.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                b2.Position = UDim2.new(0.5, 0, 0.5, 0)
                b2.Size = UDim2.new(1, -10, 1, 0)
                table.insert(
                    c["Background 1 Color"],
                    function()
                        b2.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                b2.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        b2.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                b3.CornerRadius = UDim.new(0, 4)
                b3.Name = "ColorpickBGCorner"
                b3.Parent = b2
                b4.Name = "TextColor"
                b4.Parent = b2
                b4.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                b4.BackgroundTransparency = 1.000
                b4.Position = UDim2.new(0, 10, 0, 0)
                b4.Size = UDim2.new(1, -10, 0, 35)
                b4.Font = Enum.Font.GothamBlack
                b4.Text = aY
                b4.TextSize = 14.000
                b4.TextXAlignment = Enum.TextXAlignment.Left
                b4.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        b4.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                b5.Name = "ColorVal"
                b5.Parent = b0
                b5.AnchorPoint = Vector2.new(1, 0)
                b5.BackgroundColor3 = e[a_].Color
                b5.Position = UDim2.new(1, -10, 0, 5)
                b5.Size = UDim2.new(0, 150, 0, 25)
                b6.CornerRadius = UDim.new(0, 4)
                b6.Name = "ColorValCorner"
                b6.Parent = b5
                b7.Name = "ColorValButton"
                b7.Parent = b5
                b7.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                b7.BackgroundTransparency = 1.000
                b7.Size = UDim2.new(1, 0, 1, 0)
                b7.Font = Enum.Font.SourceSans
                b7.Text = ""
                b7.TextColor3 = Color3.fromRGB(0, 0, 0)
                b7.TextSize = 14.000
                b8.Name = "Hue"
                b8.Parent = b0
                b8.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                b8.BorderSizePixel = 0
                b8.Position = UDim2.new(0, 460, 0, 40)
                b8.Size = UDim2.new(0, 25, 0, 200)
                b9.Color =
                    ColorSequence.new {
                    ColorSequenceKeypoint.new(0.00, Color3.fromRGB(255, 0, 4)),
                    ColorSequenceKeypoint.new(0.17, Color3.fromRGB(235, 7, 255)),
                    ColorSequenceKeypoint.new(0.33, Color3.fromRGB(0, 9, 189)),
                    ColorSequenceKeypoint.new(0.49, Color3.fromRGB(0, 193, 196)),
                    ColorSequenceKeypoint.new(0.66, Color3.fromRGB(0, 255, 0)),
                    ColorSequenceKeypoint.new(0.84, Color3.fromRGB(255, 247, 0)),
                    ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 0, 0))
                }
                b9.Rotation = 90
                b9.Name = "HueGra"
                b9.Parent = b8
                ba.Parent = b8
                ba.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                ba.Position = UDim2.new(0, 0, 1, 0)
                ba.Size = UDim2.new(1, 0, 0, 2)
                M.CornerRadius = UDim.new(0, 4)
                M.Parent = b8
                bb.Name = "Concac"
                bb.Parent = b0
                bb.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bb.BackgroundTransparency = 1.000
                bb.Position = UDim2.new(0, 495, 0, 40)
                bb.Size = UDim2.new(0, 115, 0, 100)
                bc.Name = "RFrame"
                bc.Parent = bb
                bc.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bc.BackgroundTransparency = 1.000
                bc.Size = UDim2.new(1, 0, 0, 25)
                bc.LayoutOrder = 0
                bd.Name = "RText"
                bd.Parent = bc
                bd.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bd.BackgroundTransparency = 1.000
                bd.Size = UDim2.new(0, 25, 0, 25)
                bd.Font = Enum.Font.GothamBold
                bd.Text = "R:"
                bd.TextColor3 = Color3.fromRGB(115, 115, 115)
                bd.TextSize = 14.000
                bd.TextXAlignment = Enum.TextXAlignment.Left
                be.Name = "RBox"
                be.Parent = bc
                be.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                be.BackgroundTransparency = 1.000
                be.Position = UDim2.new(0, 25, 0, 0)
                be.Size = UDim2.new(1, -25, 1, 0)
                be.ClearTextOnFocus = false
                be.Font = Enum.Font.GothamBold
                be.Text = "255"
                be.TextColor3 = Color3.fromRGB(255, 255, 255)
                be.TextSize = 14.000
                be.TextXAlignment = Enum.TextXAlignment.Left
                bf.Name = "GFrame"
                bf.Parent = bb
                bf.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bf.BackgroundTransparency = 1.000
                bf.Size = UDim2.new(1, 0, 0, 25)
                bf.LayoutOrder = 1
                bg.Name = "GText"
                bg.Parent = bf
                bg.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bg.BackgroundTransparency = 1.000
                bg.Size = UDim2.new(0, 25, 0, 25)
                bg.Font = Enum.Font.GothamBold
                bg.Text = "G:"
                bg.TextColor3 = Color3.fromRGB(115, 115, 115)
                bg.TextSize = 14.000
                bg.TextXAlignment = Enum.TextXAlignment.Left
                bh.Name = "GBox"
                bh.Parent = bf
                bh.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bh.BackgroundTransparency = 1.000
                bh.Position = UDim2.new(0, 25, 0, 0)
                bh.Size = UDim2.new(1, -25, 1, 0)
                bh.ClearTextOnFocus = false
                bh.Font = Enum.Font.GothamBold
                bh.Text = "255"
                bh.TextColor3 = Color3.fromRGB(255, 255, 255)
                bh.TextSize = 14.000
                bh.TextXAlignment = Enum.TextXAlignment.Left
                bi.Name = "BFrame"
                bi.Parent = bb
                bi.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bi.BackgroundTransparency = 1.000
                bi.Size = UDim2.new(1, 0, 0, 25)
                bi.LayoutOrder = 2
                bj.Name = "BText"
                bj.Parent = bi
                bj.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bj.BackgroundTransparency = 1.000
                bj.Size = UDim2.new(0, 25, 0, 25)
                bj.Font = Enum.Font.GothamBold
                bj.Text = "B:"
                bj.TextColor3 = Color3.fromRGB(115, 115, 115)
                bj.TextSize = 14.000
                bj.TextXAlignment = Enum.TextXAlignment.Left
                bk.Name = "BBox"
                bk.Parent = bi
                bk.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bk.BackgroundTransparency = 1.000
                bk.Position = UDim2.new(0, 25, 0, 0)
                bk.Size = UDim2.new(1, -25, 1, 0)
                bk.ClearTextOnFocus = false
                bk.Font = Enum.Font.GothamBold
                bk.Text = "255"
                bk.TextColor3 = Color3.fromRGB(255, 255, 255)
                bk.TextSize = 14.000
                bk.TextXAlignment = Enum.TextXAlignment.Left
                ag.Parent = bb
                ag.SortOrder = Enum.SortOrder.LayoutOrder
                bl.Name = "HexFrame"
                bl.Parent = bb
                bl.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bl.BackgroundTransparency = 1.000
                bl.Size = UDim2.new(1, 0, 0, 25)
                bl.LayoutOrder = 3
                bm.Name = "HexText"
                bm.Parent = bl
                bm.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bm.BackgroundTransparency = 1.000
                bm.Size = UDim2.new(0, 25, 0, 25)
                bm.Font = Enum.Font.GothamBold
                bm.Text = "#"
                bm.TextColor3 = Color3.fromRGB(115, 115, 115)
                bm.TextSize = 14.000
                bm.TextXAlignment = Enum.TextXAlignment.Left
                bn.Name = "HexBox"
                bn.Parent = bl
                bn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bn.BackgroundTransparency = 1.000
                bn.Position = UDim2.new(0, 25, 0, 0)
                bn.Size = UDim2.new(1, -25, 1, 0)
                bn.ClearTextOnFocus = false
                bn.Font = Enum.Font.GothamBold
                bn.Text = "FFFFFF"
                bn.TextColor3 = Color3.fromRGB(255, 255, 255)
                bn.TextSize = 14.000
                bn.TextXAlignment = Enum.TextXAlignment.Left
                aP.Name = "Linesec"
                aP.Parent = bb
                aP.AnchorPoint = Vector2.new(0.5, 1)
                aP.BorderSizePixel = 0
                aP.Position = UDim2.new(0.5, 0, 1, -2)
                aP.Size = UDim2.new(1, -10, 0, 2)
                aP.LayoutOrder = 4
                aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
                table.insert(
                    c["Section Underline Color"],
                    function()
                        aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
                    end
                )
                aQ.Transparency =
                    NumberSequence.new {
                    NumberSequenceKeypoint.new(0.00, 1.00),
                    NumberSequenceKeypoint.new(0.30, 0.25),
                    NumberSequenceKeypoint.new(0.70, 0.25),
                    NumberSequenceKeypoint.new(1.00, 1.00)
                }
                aQ.Parent = aP
                bo.Name = "CungroiF"
                bo.Parent = b0
                bo.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bo.BackgroundTransparency = 1.000
                bo.Position = UDim2.new(0, 495, 0, 145)
                bo.Size = UDim2.new(0, 115, 0, 25)
                bp.Name = "CungroiFF"
                bp.Parent = bo
                bp.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bp.BackgroundTransparency = 1.000
                bp.Size = UDim2.new(1, 0, 0, 25)
                bp.LayoutOrder = 4
                bq.Name = "TextColor"
                bq.Parent = bp
                bq.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bq.BackgroundTransparency = 1.000
                bq.Size = UDim2.new(0, 85, 0, 25)
                bq.Font = Enum.Font.GothamBold
                bq.Text = "Rainbow"
                bq.TextSize = 14.000
                bq.TextXAlignment = Enum.TextXAlignment.Left
                bq.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        bq.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                br.Name = "Setting_checkbox"
                br.Parent = bp
                br.AnchorPoint = Vector2.new(1, 0.5)
                br.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                br.BackgroundTransparency = 1.000
                br.Position = UDim2.new(1, -5, 0.5, 0)
                br.Size = UDim2.new(0, 25, 0, 25)
                br.Image = "rbxassetid://4552505888"
                br.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                table.insert(
                    c["Toggle Border Color"],
                    function()
                        br.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                    end
                )
                bs.Name = "Setting_check"
                bs.Parent = br
                bs.AnchorPoint = Vector2.new(0, 1)
                bs.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bs.BackgroundTransparency = 1.000
                bs.Position = UDim2.new(0, 0, 1, 0)
                bs.Image = "rbxassetid://4555411759"
                bs.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                table.insert(
                    c["Toggle Checked Color"],
                    function()
                        bs.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                    end
                )
                bt.Name = "Cungroitog"
                bt.Parent = bp
                bt.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bt.BackgroundTransparency = 1.000
                bt.Size = UDim2.new(1, 0, 1, 0)
                bt.Font = Enum.Font.SourceSans
                bt.Text = ""
                bt.TextColor3 = Color3.fromRGB(0, 0, 0)
                bt.TextSize = 14.000
                bu.Name = "Color"
                bu.Parent = b0
                bu.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                bu.BorderSizePixel = 0
                bu.Position = UDim2.new(0, 10, 0, 40)
                bu.Size = UDim2.new(0, 440, 0, 200)
                bu.Image = "rbxassetid://4155801252"
                bv.Name = "SelectorColor"
                bv.Parent = bu
                bv.AnchorPoint = Vector2.new(0.5, 0.5)
                bv.BackgroundColor3 = Color3.fromRGB(203, 203, 203)
                bv.BorderColor3 = Color3.fromRGB(70, 70, 70)
                bv.Position = UDim2.new(1, 0, 0, 0)
                bv.Size = UDim2.new(0, 4, 0, 4)
                bw.CornerRadius = UDim.new(0, 4)
                bw.Parent = bu
                bx.Name = "HoithoF"
                bx.Parent = b0
                bx.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bx.BackgroundTransparency = 1.000
                bx.Position = UDim2.new(0, 495, 0, 175)
                bx.Size = UDim2.new(0, 115, 0, 25)
                bx.LayoutOrder = 5
                by.Name = "HoithoF"
                by.Parent = bx
                by.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                by.BackgroundTransparency = 1.000
                by.Size = UDim2.new(1, 0, 1, 25)
                bz.Name = "TextColor"
                bz.Parent = by
                bz.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bz.BackgroundTransparency = 1.000
                bz.Size = UDim2.new(0, 85, 0, 25)
                bz.Font = Enum.Font.GothamBold
                bz.Text = "Breathing"
                bz.TextSize = 14.000
                bz.TextXAlignment = Enum.TextXAlignment.Left
                bz.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        bz.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                bA.Name = "setting_checkbox"
                bA.Parent = by
                bA.AnchorPoint = Vector2.new(1, 0)
                bA.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bA.BackgroundTransparency = 1.000
                bA.Position = UDim2.new(1, -5, 0, 0)
                bA.Size = UDim2.new(0, 25, 0, 25)
                bA.Image = "rbxassetid://4552505888"
                bA.ImageColor3 = Color3.fromRGB(131, 181, 255)
                bA.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                table.insert(
                    c["Toggle Border Color"],
                    function()
                        bA.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                    end
                )
                bB.Name = "setting_check"
                bB.Parent = bA
                bB.AnchorPoint = Vector2.new(0, 1)
                bB.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bB.BackgroundTransparency = 1.000
                bB.Position = UDim2.new(0, 0, 1, 0)
                bB.Image = "rbxassetid://4555411759"
                bB.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                table.insert(
                    c["Toggle Checked Color"],
                    function()
                        bB.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                    end
                )
                bC.Name = "Hoithoitog"
                bC.Parent = by
                bC.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bC.BackgroundTransparency = 1.000
                bC.Size = UDim2.new(1, 0, 0, 25)
                bC.Font = Enum.Font.SourceSans
                bC.Text = ""
                bC.TextColor3 = Color3.fromRGB(0, 0, 0)
                bC.TextSize = 14.000
                bD.Parent = by
                bD.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bD.BackgroundTransparency = 1.000
                bD.Position = UDim2.new(0, 0, 0, 30)
                bD.Size = UDim2.new(1, 0, 0, 25)
                bE.Parent = bD
                bE.FillDirection = Enum.FillDirection.Horizontal
                bE.SortOrder = Enum.SortOrder.LayoutOrder
                bE.Padding = UDim.new(0, 5)
                bF.Name = "Cor1"
                bF.Parent = bD
                bF.BackgroundColor3 = e[a_].Breathing.Color1
                bF.Selectable = true
                bF.Size = UDim2.new(0, 25, 0, 25)
                bG.CornerRadius = UDim.new(1, 0)
                bG.Parent = bF
                bH.Name = "BCor1"
                bH.Parent = bF
                bH.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bH.BackgroundTransparency = 1.000
                bH.Size = UDim2.new(1, 0, 1, 0)
                bH.Font = Enum.Font.SourceSans
                bH.Text = ""
                bH.TextColor3 = Color3.fromRGB(0, 0, 0)
                bH.TextSize = 14.000
                bI.Name = "Cor2"
                bI.Parent = bD
                bI.BackgroundColor3 = e[a_].Breathing.Color2
                bI.Selectable = true
                bI.Size = UDim2.new(0, 25, 0, 25)
                bJ.CornerRadius = UDim.new(1, 0)
                bJ.Parent = bI
                bK.Name = "BCor2"
                bK.Parent = bI
                bK.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                bK.BackgroundTransparency = 1.000
                bK.Size = UDim2.new(1, 0, 1, 0)
                bK.Font = Enum.Font.SourceSans
                bK.Text = ""
                bK.TextColor3 = Color3.fromRGB(0, 0, 0)
                bK.TextSize = 14.000
                local bL = false
                b7.MouseButton1Click:Connect(
                    function()
                        bL = not bL
                        local bM = bL and UDim2.new(1, 0, 0, 255) or UDim2.new(1, 0, 0, 35)
                        w:Create(b0, TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]), {Size = bM}):Play()
                    end
                )
                b7.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                local bN = game:GetService("UserInputService")
                local bO = game:GetService("RunService")
                local bP = game.Players.LocalPlayer
                local y = bP:GetMouse()
                local bQ, bR = nil, nil
                local bS = true
                local bT = 0
                local function bU(...)
                    if bS then
                        return wait(...)
                    else
                        wait()
                        return false
                    end
                end
                local function bV(g)
                    return {math.floor(g.r * 255), math.floor(g.g * 255), math.floor(g.b * 255)}
                end
                local function bW(bX)
                    bX = bX:gsub("#", ""):upper():gsub("0X", "")
                    return Color3.fromRGB(
                        tonumber(bX:sub(1, 2), 16),
                        tonumber(bX:sub(3, 4), 16),
                        tonumber(bX:sub(5, 6), 16)
                    )
                end
                local function bY(g)
                    local bZ, b_, B =
                        string.format("%X", math.floor(g.R * 255)),
                        string.format("%X", math.floor(g.G * 255)),
                        string.format("%X", math.floor(g.B * 255))
                    if #bZ < 2 then
                        bZ = "0" .. bZ
                    end
                    if #b_ < 2 then
                        b_ = "0" .. b_
                    end
                    if #B < 2 then
                        B = "0" .. B
                    end
                    return string.format("%s%s%s", bZ, b_, B)
                end
                aV, aW, aX = 1, 1, 1
                local function c0(n, B)
                    if n > B then
                        return n, B
                    else
                        return B, n
                    end
                end
                local function c1(n, B)
                    if n + B > 255 then
                        local c2, c3 = c0(n, B)
                        local a8 = 255 - c2
                        local c4, c5 = c0(a8, c3)
                        return c4 - c5
                    else
                        return n + B
                    end
                end
                function CongColor(n, B)
                    local c6, c7 = n, B
                    local c8 = math.sqrt
                    local c9 = {}
                    c9.R = 255 - c8(((255 - c6.R) ^ 2 + (255 - c7.R) ^ 2) / 2)
                    c9.G = 255 - c8(((255 - c6.G) ^ 2 + (255 - c7.G) ^ 2) / 2)
                    c9.B = 255 - c8(((255 - c6.B) ^ 2 + (255 - c7.B) ^ 2) / 2)
                    return Color3.new(c9.R, c9.G, c9.B)
                end
                local function ca(cb)
                    local c9 = cb or Color3.fromHSV(aV, aW, aX)
                    if not c9 then
                        aW, aV, aX = cb:ToHSV()
                    end
                    bn.Text = bY(c9)
                    bu.BackgroundColor3 = Color3.fromHSV(aV, 1, 1)
                    if cb then
                        bu.BackgroundColor3 = cb
                        bv.Position = UDim2.new(cb and select(3, Color3.toHSV(cb)))
                    end
                    local cc = 1 - Color3.toHSV(c9)
                    local cd = b8.Frame.Position.Y.Scale
                    if cd ~= cc and not ((cc == 0 or cc == 1) and (cd == 1 or cd == 0)) then
                        b8.Frame.Position = UDim2.fromScale(0, cc)
                    end
                    be.Text, bh.Text, bk.Text = bV(c9)[1], bV(c9)[2], bV(c9)[3]
                    b5.BackgroundColor3 = c9
                    local ce = {}
                    getgenv().UIColor[a_] = c9
                end
                ca(e[a_].Color)
                local function cf(cg)
                    if bQ then
                        bQ = bQ:Disconnect() and nil or nil
                    end
                    if bR then
                        bR = bR:Disconnect() and nil or nil
                    end
                    if cg then
                        pcall(
                            function()
                                local ch = 1 / 255
                                while bU() and aU.Cungroi do
                                    bT = ch + bT
                                    if bT > 1 then
                                        bT = 0
                                    end
                                    aV = bT
                                    ca(Color3.fromHSV(bT, 1, 1))
                                end
                            end
                        )
                    end
                end
                local ci = aU.Cungroi and UDim2.new(1, -4, 1, -4) or UDim2.new(0, 0, 0, 0)
                local cc = aU.Cungroi and UDim2.new(.5, 0, .5, 0) or UDim2.new(0, 0, 1, 0)
                local cj = aU.Cungroi and Vector2.new(.5, .5) or Vector2.new(0, 1)
                bs.Size = ci
                bs.Position = cc
                bs.AnchorPoint = cj
                spawn(
                    function()
                        cf(aU.Cungroi)
                    end
                )
                bt.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                bt.MouseButton1Click:Connect(
                    function()
                        aU.Cungroi = not aU.Cungroi
                        ci = aU.Cungroi and UDim2.new(1, -4, 1, -4) or UDim2.new(0, 0, 0, 0)
                        cc = aU.Cungroi and UDim2.new(.5, 0, .5, 0) or UDim2.new(0, 0, 1, 0)
                        cj = aU.Cungroi and Vector2.new(.5, .5) or Vector2.new(0, 1)
                        game.TweenService:Create(
                            bs,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                            {Size = ci, Position = cc, AnchorPoint = cj}
                        ):Play()
                        cf(aU.Cungroi)
                    end
                )
                bn.FocusLost:Connect(
                    function()
                        if #bn.Text > 5 then
                            local ck, cl = pcall(bW, bn.Text)
                            ca(ck and cl)
                        end
                    end
                )
                be.FocusLost:Connect(
                    function()
                        if tonumber(be.Text) > 255 then
                            be.Text = 255
                        elseif tonumber(be.Text) < 0 then
                            be.Text = 0
                        end
                        local ck, cl = pcall(Color3.fromRGB, tonumber(be.Text), tonumber(bk.Text), tonumber(bh.Text))
                        ca(ck and cl)
                    end
                )
                bh.FocusLost:Connect(
                    function()
                        if tonumber(bh.Text) > 255 then
                            bh.Text = 255
                        elseif tonumber(bh.Text) < 0 then
                            bh.Text = 0
                        end
                        local ck, cl = pcall(Color3.fromRGB, tonumber(be.Text), tonumber(bk.Text), tonumber(bh.Text))
                        ca(ck and cl)
                    end
                )
                bk.FocusLost:Connect(
                    function()
                        if tonumber(bk.Text) > 255 then
                            bk.Text = 255
                        elseif tonumber(bk.Text) < 0 then
                            bk.Text = 0
                        end
                        local ck, cl = pcall(Color3.fromRGB, tonumber(be.Text), tonumber(bk.Text), tonumber(bh.Text))
                        ca(ck and cl)
                    end
                )
                aV =
                    1 -
                    math.clamp(b8.Frame.AbsolutePosition.Y - b8.AbsolutePosition.Y, 0, b8.AbsoluteSize.Y) /
                        b8.AbsoluteSize.Y
                aW =
                    math.clamp(bu.SelectorColor.AbsolutePosition.X - bu.AbsolutePosition.X, 0, bu.AbsoluteSize.X) /
                    bu.AbsoluteSize.X
                aX =
                    1 -
                    math.clamp(bu.SelectorColor.AbsolutePosition.Y - bu.AbsolutePosition.Y, 0, bu.AbsoluteSize.Y) /
                        bu.AbsoluteSize.Y
                bu.InputBegan:Connect(
                    function(a7)
                        if a7.UserInputType == Enum.UserInputType.MouseButton1 then
                            if bQ then
                                bQ:Disconnect()
                            end
                            _ = true
                            bQ =
                                bO.RenderStepped:Connect(
                                function()
                                    local cm =
                                        math.clamp(y.X - bu.AbsolutePosition.X, 0, bu.AbsoluteSize.X) /
                                        bu.AbsoluteSize.X
                                    local cn =
                                        math.clamp(y.Y - bu.AbsolutePosition.Y, 0, bu.AbsoluteSize.Y) /
                                        bu.AbsoluteSize.Y
                                    bv.Position = UDim2.fromScale(cm, cn)
                                    aW = cm
                                    aX = 1 - cn
                                    ca()
                                end
                            )
                        end
                    end
                )
                bu.InputEnded:Connect(
                    function(a7)
                        if a7.UserInputType == Enum.UserInputType.MouseButton1 then
                            if bQ then
                                _ = false
                                bQ:Disconnect()
                            end
                        end
                    end
                )
                b8.InputBegan:Connect(
                    function(a7)
                        if a7.UserInputType == Enum.UserInputType.MouseButton1 then
                            if bR then
                                bR:Disconnect()
                            end
                            _ = true
                            bR =
                                bO.RenderStepped:Connect(
                                function()
                                    local co =
                                        math.clamp(y.Y - b8.AbsolutePosition.Y, 0, b8.AbsoluteSize.Y) /
                                        b8.AbsoluteSize.Y
                                    b8.Frame.Position = UDim2.fromScale(0, co)
                                    aV = 1 - co
                                    ca()
                                end
                            )
                        end
                    end
                )
                b8.InputEnded:Connect(
                    function(a7)
                        if a7.UserInputType == Enum.UserInputType.MouseButton1 then
                            if bR then
                                _ = false
                                bR:Disconnect()
                            end
                        end
                    end
                )
                bH.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                bK.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                bH.MouseButton1Click:Connect(
                    function()
                        bF.BackgroundColor3 = b5.BackgroundColor3
                        e[a_].Breathing.Color1 = b5.BackgroundColor3
                    end
                )
                bK.MouseButton1Click:Connect(
                    function()
                        bI.BackgroundColor3 = b5.BackgroundColor3
                        e[a_].Breathing.Color2 = b5.BackgroundColor3
                    end
                )
                bC.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                local cp = false
                spawn(
                    function()
                        while wait() do
                            if e[a_].Breathing.Toggle then
                                ca(b5.BackgroundColor3)
                            end
                        end
                    end
                )
                local function cq()
                    local cr, cs = bI.BackgroundColor3, bF.BackgroundColor3
                    local ci = e[a_].Breathing.Toggle and UDim2.new(1, -4, 1, -4) or UDim2.new(0, 0, 0, 0)
                    local cc = e[a_].Breathing.Toggle and UDim2.new(.5, 0, .5, 0) or UDim2.new(0, 0, 1, 0)
                    local cj = e[a_].Breathing.Toggle and Vector2.new(.5, .5) or Vector2.new(0, 1)
                    game.TweenService:Create(
                        bB,
                        TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                        {Size = ci, Position = cc, AnchorPoint = cj}
                    ):Play()
                    if e[a_].Breathing.Toggle then
                        local ct = game.TweenService:Create(b5, TweenInfo.new(2), {BackgroundColor3 = cs})
                        local cu = game.TweenService:Create(bu, TweenInfo.new(2), {BackgroundColor3 = cs})
                        ct:Play()
                        cu:Play()
                        ct.Completed:Connect(
                            function()
                                if e[a_].Breathing.Toggle then
                                    local cv = game.TweenService:Create(b5, TweenInfo.new(2), {BackgroundColor3 = cr})
                                    local cw = game.TweenService:Create(bu, TweenInfo.new(2), {BackgroundColor3 = cr})
                                    cv:Play()
                                    cw:Play()
                                    if e[a_].Breathing.Toggle then
                                        cv.Completed:Connect(
                                            function()
                                                ct:Play()
                                                cu:Play()
                                            end
                                        )
                                    end
                                end
                            end
                        )
                    end
                end
                spawn(
                    function()
                        cq()
                    end
                )
                bC.MouseButton1Click:Connect(
                    function()
                        e[a_].Breathing.Toggle = not e[a_].Breathing.Toggle
                        cq()
                    end
                )
            end
            function aT.CreateBox(H)
                local cx = tostring(H.Title) or ""
                local cy = tostring(H.Placeholder) or ""
                local aZ = getgenv().UIColor[H.Type] or ""
                local cz = Instance.new("Frame")
                local cA = Instance.new("UICorner")
                local cB = Instance.new("Frame")
                local cC = Instance.new("UICorner")
                local cD = Instance.new("TextLabel")
                local cE = Instance.new("Frame")
                local cF = Instance.new("UICorner")
                local cG = Instance.new("TextBox")
                local cH = Instance.new("Frame")
                cz.Name = "BoxFrame"
                cz.Parent = aM
                cz.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                cz.BackgroundTransparency = 1.000
                cz.Position = UDim2.new(0, 0, 0.208333328, 0)
                cz.Size = UDim2.new(1, 0, 0, 60)
                cA.CornerRadius = UDim.new(0, 4)
                cA.Name = "BoxCorner"
                cA.Parent = cz
                cB.Name = "Background1"
                cB.Parent = cz
                cB.AnchorPoint = Vector2.new(0.5, 0.5)
                cB.Position = UDim2.new(0.5, 0, 0.5, 0)
                cB.Size = UDim2.new(1, -10, 1, 0)
                cB.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        cB.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                cB.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        cB.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cC.CornerRadius = UDim.new(0, 4)
                cC.Name = "ButtonCorner"
                cC.Parent = cB
                cD.Name = "TextColor"
                cD.Parent = cB
                cD.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                cD.BackgroundTransparency = 1.000
                cD.Position = UDim2.new(0, 10, 0, 0)
                cD.Size = UDim2.new(1, -10, 0.5, 0)
                cD.Font = Enum.Font.GothamBlack
                cD.Text = cx
                cD.TextSize = 14.000
                cD.TextXAlignment = Enum.TextXAlignment.Left
                cD.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        cD.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cE.Name = "Background2"
                cE.Parent = cB
                cE.AnchorPoint = Vector2.new(1, 0.5)
                cE.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                cE.ClipsDescendants = true
                cE.Position = UDim2.new(1, -5, 0, 40)
                cE.Size = UDim2.new(1, -10, 0, 25)
                table.insert(
                    c["Text Color"],
                    function()
                        cE.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                cF.CornerRadius = UDim.new(0, 4)
                cF.Name = "ButtonCorner"
                cF.Parent = cE
                cG.Name = "TextColorPlaceholder"
                cG.Parent = cE
                cG.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                cG.BackgroundTransparency = 1.000
                cG.Position = UDim2.new(0, 5, 0, 0)
                cG.Size = UDim2.new(1, -5, 1, 0)
                cG.Font = Enum.Font.GothamBold
                cG.PlaceholderText = cy
                cG.Text = ""
                cG.TextSize = 14.000
                cG.TextXAlignment = Enum.TextXAlignment.Left
                cG.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                cG.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Placeholder Text Color"],
                    function()
                        cG.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                    end
                )
                table.insert(
                    c["Text Color"],
                    function()
                        cG.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cH.Name = "Setting_Lineeeee"
                cH.Parent = cE
                cH.BackgroundTransparency = 1.000
                cH.Position = UDim2.new(0, 0, 1, -2)
                cH.Size = UDim2.new(1, 0, 0, 6)
                cH.BackgroundColor3 = getgenv().UIColor["Textbox Highlight Color"]
                table.insert(
                    c["Textbox Highlight Color"],
                    function()
                        cH.BackgroundColor3 = getgenv().UIColor["Textbox Highlight Color"]
                    end
                )
                cG.Focused:Connect(
                    function()
                        w:Create(
                            cH,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundTransparency = 0}
                        ):Play()
                    end
                )
                cG.Focused:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                cG.FocusLost:Connect(
                    function()
                        w:Create(
                            cH,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundTransparency = 1}
                        ):Play()
                        if cG.Text ~= "" then
                            getgenv().UIColor[H.Type] = cG.Text
                            if H.Type == "Background Image" then
                                u.ReloadMain(cG.Text)
                            end
                        end
                    end
                )
                local cI = {}
                if aZ then
                    cG.Text = aZ
                    getgenv().UIColor[H.Type] = aZ
                end
                function cI.SetValue(r)
                    cG.Text = r
                    getgenv().UIColor[H.Type] = r
                end
                return cI
            end
            function aT.CreateSlider(H)
                local cx = tostring(H.Title) or ""
                local cJ = tonumber(H.Min) or 0
                local cK = tonumber(H.Max) or 100
                local cL = H.Precise or false
                local cM = getgenv().UIColor[H.Type] or 0
                local cN = function(v)
                    getgenv().UIColor[H.Type] = v
                end
                local cO = 600
                local cP = Instance.new("Frame")
                local cQ = Instance.new("UICorner")
                local cR = Instance.new("Frame")
                local cS = Instance.new("UICorner")
                local cT = Instance.new("TextLabel")
                local cU = Instance.new("Frame")
                local cV = Instance.new("TextButton")
                local cW = Instance.new("UICorner")
                local cX = Instance.new("Frame")
                local cY = Instance.new("UICorner")
                local cZ = Instance.new("Frame")
                local c_ = Instance.new("UICorner")
                local d0 = Instance.new("TextBox")
                cP.Name = cx .. "buda"
                cP.Parent = aM
                cP.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                cP.BackgroundTransparency = 1.000
                cP.Position = UDim2.new(0, 0, 0.208333328, 0)
                cP.Size = UDim2.new(1, 0, 0, 50)
                cQ.CornerRadius = UDim.new(0, 4)
                cQ.Name = "SliderCorner"
                cQ.Parent = cP
                cR.Name = "Background1"
                cR.Parent = cP
                cR.AnchorPoint = Vector2.new(0.5, 0.5)
                cR.Position = UDim2.new(0.5, 0, 0.5, 0)
                cR.Size = UDim2.new(1, -10, 1, 0)
                cR.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        cR.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                cR.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        cR.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cS.CornerRadius = UDim.new(0, 4)
                cS.Name = "SliderBGCorner"
                cS.Parent = cR
                cT.Name = "TextColor"
                cT.Parent = cR
                cT.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                cT.BackgroundTransparency = 1.000
                cT.Position = UDim2.new(0, 10, 0, 0)
                cT.Size = UDim2.new(1, -10, 0, 25)
                cT.Font = Enum.Font.GothamBlack
                cT.Text = cx
                cT.TextSize = 14.000
                cT.TextXAlignment = Enum.TextXAlignment.Left
                cT.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        cT.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cU.Name = "SliderBar"
                cU.Parent = cP
                cU.AnchorPoint = Vector2.new(.5, 0.5)
                cU.Position = UDim2.new(.5, 0, 0.5, 14)
                cU.Size = UDim2.new(0, 600, 0, 6)
                cU.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        cU.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                cV.Name = "SliderButton "
                cV.Parent = cU
                cV.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                cV.BackgroundTransparency = 1.000
                cV.Size = UDim2.new(1, 0, 1, 0)
                cV.Font = Enum.Font.GothamBold
                cV.Text = ""
                cV.TextColor3 = Color3.fromRGB(230, 230, 230)
                cV.TextSize = 14.000
                cW.CornerRadius = UDim.new(1, 0)
                cW.Name = "SliderBarCorner"
                cW.Parent = cU
                cX.Name = "Bar"
                cX.BorderSizePixel = 0
                cX.Parent = cU
                cX.Size = UDim2.new(0, 0, 1, 0)
                cX.BackgroundColor3 = getgenv().UIColor["Slider Line Color"]
                table.insert(
                    c["Slider Line Color"],
                    function()
                        cX.BackgroundColor3 = getgenv().UIColor["Slider Line Color"]
                    end
                )
                cY.CornerRadius = UDim.new(1, 0)
                cY.Name = "BarCorner"
                cY.Parent = cX
                cZ.Name = "Background2"
                cZ.Parent = cP
                cZ.AnchorPoint = Vector2.new(1, 0)
                cZ.Position = UDim2.new(1, -10, 0, 5)
                cZ.Size = UDim2.new(0, 150, 0, 25)
                cZ.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        cZ.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                c_.CornerRadius = UDim.new(0, 4)
                c_.Name = "Sliderbox"
                c_.Parent = cZ
                d0.Name = "TextColor"
                d0.Parent = cZ
                d0.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                d0.BackgroundTransparency = 1.000
                d0.Size = UDim2.new(1, 0, 1, 0)
                d0.Font = Enum.Font.GothamBold
                d0.Text = ""
                d0.TextSize = 14.000
                d0.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        d0.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cV.MouseEnter:Connect(
                    function()
                        w:Create(
                            cX,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundColor3 = getgenv().UIColor["Slider Highlight Color"]}
                        ):Play()
                    end
                )
                cV.MouseLeave:Connect(
                    function()
                        w:Create(
                            cX,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundColor3 = getgenv().UIColor["Slider Line Color"]}
                        ):Play()
                    end
                )
                local y = game.Players.LocalPlayer:GetMouse()
                if cM then
                    if cM <= cJ then
                        cM = cJ
                    elseif cM >= cK then
                        cM = cK
                    end
                    cX.Size = UDim2.new(1 - (cK - cM) / (cK - cJ), 0, 0, 6)
                    d0.Text = cM
                    cN(cM)
                end
                cV.MouseButton1Down:Connect(
                    function()
                        local d1 =
                            cL and
                            tonumber(
                                string.format(
                                    "%.1f",
                                    (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                )
                            ) or
                            math.floor((tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ))
                        pcall(
                            function()
                                cN(d1)
                                d0.Text = d1
                            end
                        )
                        cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                        moveconnection =
                            y.Move:Connect(
                            function()
                                local d1 =
                                    cL and
                                    tonumber(
                                        string.format(
                                            "%.1f",
                                            (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                        )
                                    ) or
                                    math.floor((tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ))
                                pcall(
                                    function()
                                        cN(d1)
                                        d0.Text = d1
                                    end
                                )
                                cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                            end
                        )
                        releaseconnection =
                            x.InputEnded:Connect(
                            function(d2)
                                if d2.UserInputType == Enum.UserInputType.MouseButton1 then
                                    local d1 =
                                        cL and
                                        tonumber(
                                            string.format(
                                                "%.1f",
                                                (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                            )
                                        ) or
                                        math.floor(
                                            (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                        )
                                    pcall(
                                        function()
                                            cN(d1)
                                            d0.Text = d1
                                        end
                                    )
                                    cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                                    moveconnection:Disconnect()
                                    releaseconnection:Disconnect()
                                end
                            end
                        )
                    end
                )
                local function d3(r)
                    if tonumber(r) <= cJ then
                        cX.Size = UDim2.new(0, 0 * cO, 0, 6)
                        d0.Text = cJ
                        cN(tonumber(cJ))
                    elseif tonumber(r) >= cK then
                        cX.Size = UDim2.new(0, cK / cK * cO, 0, 6)
                        d0.Text = cK
                        cN(tonumber(cK))
                    else
                        cX.Size = UDim2.new(1 - (cK - r) / (cK - cJ), 0, 0, 6)
                        cN(tonumber(r))
                    end
                end
                d0.FocusLost:Connect(
                    function()
                        d3(d0.Text)
                    end
                )
                local d4 = {}
                function d4.SetValue(r)
                    d3(r)
                end
                return d4
            end
            return aT
        end
        return aK
    end
    local d5 = t.CreateCustomColor()
    local d6 = d5.CreateSection("Main")
    d6.CreateColorPicker({Title = "Border Color", Type = "Border Color"})
    d6.CreateColorPicker({Title = "Click Effect Color", Type = "Click Effect Color"})
    d6.CreateColorPicker({Title = "Setting Icon Color", Type = "Setting Icon Color"})
    d6.CreateBox({Title = "Logo Image", Placeholder = "URL Here (PNG only), Recommended 128x128", Type = "Logo Image"})
    local d7 = d5.CreateSection("Search")
    d7.CreateColorPicker({Title = "Search Icon Color", Type = "Search Icon Color"})
    d7.CreateColorPicker({Title = "Search Icon Highlight Color", Type = "Search Icon Highlight Color"})
    local d8 = d5.CreateSection("Text")
    d8.CreateColorPicker({Title = "GUI Text Color", Type = "GUI Text Color"})
    d8.CreateColorPicker({Title = "Text Color", Type = "Text Color"})
    d8.CreateColorPicker({Title = "Placeholder Text Color", Type = "Placeholder Text Color"})
    d8.CreateColorPicker({Title = "Title Text Color", Type = "Title Text Color"})
    local d9 = d5.CreateSection("Background")
    d9.CreateColorPicker({Title = "Background 1 Color", Type = "Background 1 Color"})
    d9.CreateSlider(
        {
            Title = "Background 1 Transparency",
            Type = "Background 1 Transparency",
            Min = 0,
            Max = 1,
            Default = 0,
            Precise = true
        }
    )
    d9.CreateColorPicker({Title = "Background 2 Color", Type = "Background 2 Color"})
    d9.CreateColorPicker({Title = "Background 3 Color", Type = "Background 3 Color"})
    d9.CreateBox(
        {
            Title = "Background Image",
            Placeholder = "URL Here (WEBM / PNG only), Recommended 1280x720",
            Type = "Background Image"
        }
    )
    local da = d5.CreateSection("Page")
    da.CreateColorPicker({Title = "Page Selected Color", Type = "Page Selected Color"})
    local db = d5.CreateSection("Section")
    db.CreateColorPicker({Title = "Section Text Color", Type = "Section Text Color"})
    db.CreateColorPicker({Title = "Section Underline Color", Type = "Section Underline Color"})
    local dc = d5.CreateSection("Toggle")
    dc.CreateColorPicker({Title = "Toggle Border Color", Type = "Toggle Border Color"})
    dc.CreateColorPicker({Title = "Toggle Checked Color", Type = "Toggle Checked Color"})
    dc.CreateColorPicker({Title = "Toggle Desc Color", Type = "Toggle Desc Color"})
    local dd = d5.CreateSection("Button")
    dd.CreateColorPicker({Title = "Button Color", Type = "Button Color"})
    local dd = d5.CreateSection("Label")
    dd.CreateColorPicker({Title = "Label Color", Type = "Label Color"})
    local de = d5.CreateSection("Dropdown")
    de.CreateColorPicker({Title = "Dropdown Icon Color", Type = "Dropdown Icon Color"})
    de.CreateColorPicker({Title = "Dropdown Selected Color", Type = "Dropdown Selected Color"})
    local df = d5.CreateSection("Textbox")
    df.CreateColorPicker({Title = "Textbox Highlight Color", Type = "Textbox Highlight Color"})
    local dg = d5.CreateSection("Box")
    dg.CreateColorPicker({Title = "Box Highlight Color", Type = "Box Highlight Color"})
    local dh = d5.CreateSection("Slider")
    dh.CreateColorPicker({Title = "Slider Line Color", Type = "Slider Line Color"})
    dh.CreateColorPicker({Title = "Slider Highlight Color", Type = "Slider Highlight Color"})
    local di = d5.CreateSection("Animation")
    di.CreateSlider(
        {
            Title = "Tween Animation 1 Speed",
            Type = "Tween Animation 1 Speed",
            Min = 0,
            Max = 0.75,
            Default = 0.25,
            Precise = true
        }
    )
    di.CreateSlider(
        {
            Title = "Tween Animation 2 Speed",
            Type = "Tween Animation 2 Speed",
            Min = 0,
            Max = 1,
            Default = 0.5,
            Precise = true
        }
    )
    di.CreateSlider(
        {
            Title = "Tween Animation 3 Speed",
            Type = "Tween Animation 3 Speed",
            Min = 0,
            Max = 0.5,
            Default = 0.1,
            Precise = true
        }
    )
    local dj = {}
    local dk = -1
    local dl = -1
    local dm = 1
    function dj.CreatePage(H)
        local dn = tostring(H.Page_Name)
        local dp = tostring(H.Page_Title)
        dl = dl + 1
        dk = dk + 1
        local dq = Instance.new("Frame")
        local ba = Instance.new("Frame")
        local dr = Instance.new("UICorner")
        local ds = Instance.new("Frame")
        local dt = Instance.new("Frame")
        local du = Instance.new("UICorner")
        local dv = Instance.new("Frame")
        local dw = Instance.new("TextLabel")
        local dx = Instance.new("TextButton")
        dq.Name = dn .. "_Control"
        dq.Parent = af
        dq.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dq.BackgroundTransparency = 1.000
        dq.Size = UDim2.new(1, -10, 0, 25)
        dq.LayoutOrder = dk
        ba.Parent = dq
        ba.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        ba.BackgroundTransparency = 1.000
        ba.Position = UDim2.new(0, 5, 0, 0)
        ba.Size = UDim2.new(1, -5, 1, 0)
        dr.CornerRadius = UDim.new(0, 4)
        dr.Name = "TabNameCorner"
        dr.Parent = ba
        ds.Name = "Line"
        ds.Parent = ba
        ds.AnchorPoint = Vector2.new(0, 0.5)
        ds.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        ds.BackgroundTransparency = 1.000
        ds.Position = UDim2.new(0, 0, 0.5, 0)
        ds.Size = UDim2.new(0, 14, 1, 0)
        dt.Name = "PageInLine"
        dt.Parent = ds
        dt.AnchorPoint = Vector2.new(0.5, 0.5)
        dt.BorderSizePixel = 0
        dt.Position = UDim2.new(0.5, 0, 0.5, 0)
        dt.Size = UDim2.new(1, -10, 0, 0)
        dt.BackgroundColor3 = getgenv().UIColor["Page Selected Color"]
        table.insert(
            c["Page Selected Color"],
            function()
                dt.BackgroundColor3 = getgenv().UIColor["Page Selected Color"]
            end
        )
        du.Name = "LineCorner"
        du.Parent = dt
        dv.Name = "TabTitleContainer"
        dv.Parent = ba
        dv.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dv.BackgroundTransparency = 1.000
        dv.Position = UDim2.new(0, 15, 0, 0)
        dv.Size = UDim2.new(1, -15, 1, 0)
        dw.Name = "GUITextColor"
        dw.Parent = dv
        dw.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dw.BackgroundTransparency = 1.000
        dw.Size = UDim2.new(1, 0, 1, 0)
        dw.Font = Enum.Font.GothamBold
        dw.Text = dn
        dw.TextColor3 = Color3.fromRGB(230, 230, 230)
        dw.TextSize = 14.000
        dw.TextXAlignment = Enum.TextXAlignment.Left
        dw.TextColor3 = getgenv().UIColor["GUI Text Color"]
        table.insert(
            c["GUI Text Color"],
            function()
                dw.TextColor3 = getgenv().UIColor["GUI Text Color"]
            end
        )
        dx.Name = "PageButton"
        dx.Parent = dq
        dx.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dx.BackgroundTransparency = 1.000
        dx.Size = UDim2.new(1, 0, 1, 0)
        dx.Font = Enum.Font.SourceSans
        dx.Text = ""
        dx.TextColor3 = Color3.fromRGB(0, 0, 0)
        dx.TextSize = 14.000
        local dy = Instance.new("Frame")
        local M = Instance.new("UICorner")
        local dz = Instance.new("TextLabel")
        local dA = Instance.new("ScrollingFrame")
        local dB = Instance.new("UIListLayout")
        local dC = dm
        dm = dm + 1
        dy.Name = "Page" .. dC
        dy.Parent = ai
        dy.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
        dy.Position = UDim2.new(0, 190, 0, 30)
        dy.Size = UDim2.new(0, 435, 0, 325)
        dy.LayoutOrder = dl
        table.insert(
            c["Background 1 Color"],
            function()
                dy.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
            end
        )
        dy.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
        table.insert(
            c["Background 1 Transparency"],
            function()
                dy.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
            end
        )
        M.CornerRadius = UDim.new(0, 4)
        M.Parent = dy
        dz.Name = "GUITextColor"
        dz.Parent = dy
        dz.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dz.BackgroundTransparency = 1.000
        dz.Position = UDim2.new(0, 5, 0, 0)
        dz.Size = UDim2.new(1, 0, 0, 25)
        dz.Font = Enum.Font.GothamBold
        dz.Text = dp
        dz.TextSize = 16.000
        dz.TextXAlignment = Enum.TextXAlignment.Left
        dz.TextColor3 = getgenv().UIColor["GUI Text Color"]
        table.insert(
            c["GUI Text Color"],
            function()
                dz.TextColor3 = getgenv().UIColor["GUI Text Color"]
            end
        )
        dA.Name = "PageList"
        dA.Parent = dy
        dA.Active = true
        dA.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
        dA.BackgroundTransparency = 1.000
        dA.BorderColor3 = Color3.fromRGB(27, 42, 53)
        dA.BorderSizePixel = 0
        dA.Position = UDim2.new(0, 5, 0, 30)
        dA.Size = UDim2.new(1, -10, 1, -30)
        dA.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        dA.ScrollBarThickness = 5
        dA.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        dB.Name = "Pagelistlayout"
        dB.Parent = dA
        dB.SortOrder = Enum.SortOrder.LayoutOrder
        dB.Padding = UDim.new(0, 5)
        dB:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
            function()
                dA.CanvasSize = UDim2.new(0, 0, 0, dB.AbsoluteContentSize.Y + 5)
            end
        )
        local dD = Instance.new("Frame")
        local aA = Instance.new("UICorner")
        local aB = Instance.new("Frame")
        local aC = Instance.new("ImageLabel")
        local aD = Instance.new("TextButton")
        local dE = Instance.new("TextBox")
        dD.Name = "Background2"
        dD.Parent = dy
        dD.AnchorPoint = Vector2.new(1, 0)
        dD.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
        dD.Position = UDim2.new(1, -5, 0, 5)
        dD.Size = UDim2.new(0, 20, 0, 20)
        dD.ClipsDescendants = true
        table.insert(
            c["Background 2 Color"],
            function()
                dD.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
            end
        )
        aA.CornerRadius = UDim.new(0, 2)
        aA.Name = "PageSearchCorner"
        aA.Parent = dD
        aB.Name = "SearchFrame"
        aB.Parent = dD
        aB.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        aB.BackgroundTransparency = 1.000
        aB.Size = UDim2.new(0, 20, 0, 20)
        aC.Name = "SearchIcon"
        aC.Parent = aB
        aC.AnchorPoint = Vector2.new(0.5, 0.5)
        aC.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        aC.BackgroundTransparency = 1.000
        aC.Position = UDim2.new(0.5, 0, 0.5, 0)
        aC.Size = UDim2.new(0, 16, 0, 16)
        aC.Image = "rbxassetid://8154282545"
        aC.ImageColor3 = getgenv().UIColor["Search Icon Color"]
        table.insert(
            c["Search Icon Color"],
            function()
                aC.ImageColor3 = getgenv().UIColor["Search Icon Color"]
            end
        )
        aD.Name = "active"
        aD.Parent = aB
        aD.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        aD.BackgroundTransparency = 1.000
        aD.Size = UDim2.new(1, 0, 1, 0)
        aD.Font = Enum.Font.SourceSans
        aD.Text = ""
        aD.TextColor3 = Color3.fromRGB(0, 0, 0)
        aD.TextSize = 14.000
        dE.Name = "TextColorPlaceholder"
        dE.Parent = dD
        dE.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        dE.BackgroundTransparency = 1.000
        dE.Position = UDim2.new(0, 30, 0, 0)
        dE.Size = UDim2.new(1, -30, 1, 0)
        dE.Font = Enum.Font.GothamBold
        dE.Text = ""
        dE.TextSize = 14.000
        dE.TextXAlignment = Enum.TextXAlignment.Left
        dE.PlaceholderText = "Search Section name"
        dE.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
        dE.TextColor3 = getgenv().UIColor["Text Color"]
        table.insert(
            c["Placeholder Text Color"],
            function()
                dE.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
            end
        )
        table.insert(
            c["Text Color"],
            function()
                dE.TextColor3 = getgenv().UIColor["Text Color"]
            end
        )
        local dF = false
        aD.MouseEnter:Connect(
            function()
                w:Create(
                    aC,
                    TweenInfo.new(getgenv().UIColor["Tween Animation 3 Speed"]),
                    {ImageColor3 = getgenv().UIColor["Search Icon Highlight Color"]}
                ):Play()
            end
        )
        aD.MouseLeave:Connect(
            function()
                w:Create(
                    aC,
                    TweenInfo.new(getgenv().UIColor["Tween Animation 3 Speed"]),
                    {ImageColor3 = getgenv().UIColor["Search Icon Color"]}
                ):Play()
            end
        )
        aD.MouseButton1Click:Connect(
            function()
                u.ButtonEffect()
            end
        )
        dE.Focused:Connect(
            function()
                u.ButtonEffect()
            end
        )
        aD.MouseButton1Click:Connect(
            function()
                dF = not dF
                local aG = dF and UDim2.new(0, 175, 0, 20) or UDim2.new(0, 20, 0, 20)
                game.TweenService:Create(dD, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = aG}):Play(

                )
            end
        )
        local function dG()
            for a, v in next, dA:GetChildren() do
                if not v:IsA("UIListLayout") then
                    v.Visible = false
                end
            end
        end
        local function dH()
            for n, B in pairs(dA:GetChildren()) do
                if not B:IsA("UIListLayout") then
                    if string.find(string.lower(B.Name), string.lower(dE.Text)) then
                        B.Visible = true
                    end
                end
            end
        end
        dE:GetPropertyChangedSignal("Text"):Connect(
            function()
                dG()
                dH()
            end
        )
        for a, v in pairs(af:GetChildren()) do
            if not v:IsA("UIListLayout") then
                if a == 2 then
                    v.Frame.Line.PageInLine.Size = UDim2.new(1, -10, 1, -10)
                    oldlay = v.LayoutOrder
                    oldobj = v
                end
            end
        end
        dx.MouseButton1Click:Connect(
            function()
                spawn(
                    function()
                        u.ButtonEffect()
                    end
                )
                if tostring(aj.CurrentPage) == dy.Name then
                    return
                end
                for a, v in pairs(ai:GetChildren()) do
                    if not v:IsA("UIPageLayout") and not v:IsA("UICorner") then
                        v.Visible = false
                    end
                end
                dy.Visible = true
                aj:JumpTo(dy)
                for a, v in next, af:GetChildren() do
                    if not v:IsA("UIListLayout") then
                        if v.Name == dn .. "_Control" then
                            if v.LayoutOrder > oldlay then
                                oldobj.Active = false
                                w:Create(
                                    oldobj.Frame.Line.PageInLine,
                                    TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                                    {
                                        Size = UDim2.new(1, -10, 0, 0),
                                        Position = UDim2.new(0.5, 0, 1, 0),
                                        AnchorPoint = Vector2.new(.5, 1)
                                    }
                                ):Play()
                                v.Frame.Line.PageInLine.Position = UDim2.new(0.5, 0, 0, 0)
                                v.Frame.Line.PageInLine.AnchorPoint = Vector2.new(.5, 0)
                                wait(getgenv().UIColor["Tween Animation 1 Speed"])
                                w:Create(
                                    v.Frame.Line.PageInLine,
                                    TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                                    {
                                        Size = UDim2.new(1, -10, 1, -10),
                                        Position = UDim2.new(0.5, 0, .5, 0),
                                        AnchorPoint = Vector2.new(.5, .5)
                                    }
                                ):Play()
                                v.Active = true
                                oldobj = v
                                oldlay = v.LayoutOrder
                            else
                                oldobj.Active = false
                                w:Create(
                                    oldobj.Frame.Line.PageInLine,
                                    TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                                    {
                                        Size = UDim2.new(1, -10, 0, 0),
                                        Position = UDim2.new(0.5, 0, 0, 0),
                                        AnchorPoint = Vector2.new(.5, 0)
                                    }
                                ):Play()
                                v.Frame.Line.PageInLine.Position = UDim2.new(0.5, 0, 1, 0)
                                v.Frame.Line.PageInLine.AnchorPoint = Vector2.new(.5, 1)
                                wait(getgenv().UIColor["Tween Animation 1 Speed"])
                                w:Create(
                                    v.Frame.Line.PageInLine,
                                    TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                                    {
                                        Size = UDim2.new(1, -10, 1, -10),
                                        Position = UDim2.new(0.5, 0, .5, 0),
                                        AnchorPoint = Vector2.new(.5, .5)
                                    }
                                ):Play()
                                v.Active = true
                                oldobj = v
                                oldlay = v.LayoutOrder
                            end
                        end
                    end
                end
            end
        )
        local dI = {}
        function dI.CreateSection(aL)
            local aM = Instance.new("Frame")
            local M = Instance.new("UICorner")
            local aN = Instance.new("Frame")
            local aO = Instance.new("TextLabel")
            local aP = Instance.new("Frame")
            local aQ = Instance.new("UIGradient")
            local aR = Instance.new("UIListLayout")
            aM.Name = aL .. "_Dot"
            aM.Parent = dA
            aM.Size = UDim2.new(0, 415, 0, 100)
            aM.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
            table.insert(
                c["Background 3 Color"],
                function()
                    aM.BackgroundColor3 = getgenv().UIColor["Background 3 Color"]
                end
            )
            aM.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
            table.insert(
                c["Background 1 Transparency"],
                function()
                    aM.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                end
            )
            M.CornerRadius = UDim.new(0, 4)
            M.Parent = aM
            aN.Name = "Topsec"
            aN.Parent = aM
            aN.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
            aN.BackgroundTransparency = 1.000
            aN.Size = UDim2.new(0, 415, 0, 30)
            aO.Name = "Sectiontitle"
            aO.Parent = aN
            aO.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
            aO.BackgroundTransparency = 1.000
            aO.Size = UDim2.new(1, 0, 1, 0)
            aO.Font = Enum.Font.GothamBold
            aO.Text = aL
            aO.TextSize = 14.000
            aO.TextColor3 = getgenv().UIColor["Section Text Color"]
            table.insert(
                c["Section Text Color"],
                function()
                    aO.TextColor3 = getgenv().UIColor["Section Text Color"]
                end
            )
            aP.Name = "Linesec"
            aP.Parent = aN
            aP.AnchorPoint = Vector2.new(0.5, 1)
            aP.BorderSizePixel = 0
            aP.Position = UDim2.new(0.5, 0, 1, -2)
            aP.Size = UDim2.new(1, -10, 0, 2)
            aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
            table.insert(
                c["Section Underline Color"],
                function()
                    aP.BackgroundColor3 = getgenv().UIColor["Section Underline Color"]
                end
            )
            aQ.Transparency =
                NumberSequence.new {
                NumberSequenceKeypoint.new(0.00, 1.00),
                NumberSequenceKeypoint.new(0.50, 0.00),
                NumberSequenceKeypoint.new(0.51, 0.02),
                NumberSequenceKeypoint.new(1.00, 1.00)
            }
            aQ.Parent = aP
            aR.Name = "SectionList"
            aR.Parent = aM
            aR.SortOrder = Enum.SortOrder.LayoutOrder
            aR.Padding = UDim.new(0, 5)
            aR:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
                function()
                    aM.Size = UDim2.new(1, -5, 0, aR.AbsoluteContentSize.Y + 5)
                end
            )
            local dJ = {}
            function dJ.CreateToggle(H, cN)
                local aY = tostring(H.Title)
                local I = H.Desc
                local aZ = H.Default
                local cN = cN or function()
                    end
                local dK = Instance.new("Frame")
                local dL = Instance.new("Frame")
                local br = Instance.new("ImageLabel")
                local bs = Instance.new("ImageLabel")
                local dM = Instance.new("TextLabel")
                local dN = Instance.new("TextLabel")
                local dO = Instance.new("Frame")
                local dP = Instance.new("UICorner")
                local dQ = Instance.new("TextButton")
                local dR = Instance.new("UIListLayout")
                dK.Name = "ToggleFrame"
                dK.Parent = aM
                dK.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dK.BackgroundTransparency = 1.000
                dK.Position = UDim2.new(0, 0, 0.300000012, 0)
                dK.Size = UDim2.new(1, 0, 0, 0)
                dK.AutomaticSize = Enum.AutomaticSize.Y
                dL.Name = "TogFrame1"
                dL.Parent = dK
                dL.AnchorPoint = Vector2.new(0.5, 0.5)
                dL.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dL.BackgroundTransparency = 1.000
                dL.Position = UDim2.new(0.5, 0, 0.5, 0)
                dL.Size = UDim2.new(1, -10, 0, 0)
                dL.AutomaticSize = Enum.AutomaticSize.Y
                br.Name = "checkbox"
                br.Parent = dL
                br.AnchorPoint = Vector2.new(1, 0.5)
                br.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                br.BackgroundTransparency = 1.000
                br.Position = UDim2.new(1, -5, 0.5, 3)
                br.Size = UDim2.new(0, 25, 0, 25)
                br.Image = "rbxassetid://4552505888"
                br.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                table.insert(
                    c["Toggle Border Color"],
                    function()
                        br.ImageColor3 = getgenv().UIColor["Toggle Border Color"]
                    end
                )
                bs.Name = "check"
                bs.Parent = br
                bs.AnchorPoint = Vector2.new(0, 1)
                bs.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                bs.BackgroundTransparency = 1.000
                bs.Position = UDim2.new(0, 0, 1, 0)
                bs.Image = "rbxassetid://4555411759"
                bs.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                table.insert(
                    c["Toggle Checked Color"],
                    function()
                        bs.ImageColor3 = getgenv().UIColor["Toggle Checked Color"]
                    end
                )
                local cac = 5
                if I then
                    cac = 0
                    dM.Name = "ToggleDesc"
                    dM.Parent = dL
                    dM.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                    dM.BackgroundTransparency = 1.000
                    dM.Position = UDim2.new(0, 15, 0, 20)
                    dM.Size = UDim2.new(1, -50, 0, 0)
                    dM.Font = Enum.Font.GothamBlack
                    dM.Text = I
                    dM.TextSize = 13.000
                    dM.TextWrapped = true
                    dM.TextXAlignment = Enum.TextXAlignment.Left
                    dM.RichText = true
                    dM.AutomaticSize = Enum.AutomaticSize.Y
                    dM.TextColor3 = getgenv().UIColor["Toggle Desc Color"]
                    table.insert(
                        c["Toggle Desc Color"],
                        function()
                            dM.TextColor3 = getgenv().UIColor["Toggle Desc Color"]
                        end
                    )
                else
                    dM.Text = ""
                end
                dN.Name = "TextColor"
                dN.Parent = dL
                dN.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dN.BackgroundTransparency = 1.000
                dN.Position = UDim2.new(0, 10, 0, cac)
                dN.Size = UDim2.new(1, -10, 0, 20)
                dN.Font = Enum.Font.GothamBlack
                dN.Text = aY
                dN.TextSize = 14.000
                dN.TextXAlignment = Enum.TextXAlignment.Left
                dN.TextYAlignment = Enum.TextYAlignment.Center
                dN.RichText = true
                dN.AutomaticSize = Enum.AutomaticSize.Y
                dN.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        dN.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                dO.Name = "Background1"
                dO.Parent = dL
                dO.Size = UDim2.new(1, 0, 1, 6)
                dO.ZIndex = 0
                dO.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        dO.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                dO.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        dO.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                dP.CornerRadius = UDim.new(0, 4)
                dP.Name = "ToggleCorner"
                dP.Parent = dO
                dQ.Name = "ToggleButton"
                dQ.Parent = dL
                dQ.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dQ.BackgroundTransparency = 1.000
                dQ.Size = UDim2.new(1, 0, 1, 6)
                dQ.Font = Enum.Font.SourceSans
                dQ.Text = ""
                dQ.TextColor3 = Color3.fromRGB(0, 0, 0)
                dQ.TextSize = 14.000
                dR.Name = "ToggleList"
                dR.Parent = dK
                dR.HorizontalAlignment = Enum.HorizontalAlignment.Center
                dR.SortOrder = Enum.SortOrder.LayoutOrder
                dR.VerticalAlignment = Enum.VerticalAlignment.Center
                dR.Padding = UDim.new(0, 5)
                local function dS(dT)
                    local ci = dT and UDim2.new(1, -4, 1, -4) or UDim2.new(0, 0, 0, 0)
                    local cc = dT and UDim2.new(.5, 0, .5, 0) or UDim2.new(0, 0, 1, 0)
                    local cj = dT and Vector2.new(.5, .5) or Vector2.new(0, 1)
                    game.TweenService:Create(
                        bs,
                        TweenInfo.new(getgenv().UIColor["Tween Animation 1 Speed"]),
                        {Size = ci, Position = cc, AnchorPoint = cj}
                    ):Play()
                    cN(dT)
                end
                if cN then
                    dS(aZ)
                end
                dQ.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                dQ.MouseButton1Down:Connect(
                    function()
                        aZ = not aZ
                        dS(aZ)
                    end
                )
                local dU = {}
                function dU.SetStage(d1)
                    dS(d1)
                end
                return dU
            end
            function dJ.CreateButton(H, cN)
                local aY = H.Title
                local cN = cN or function()
                    end
                local dV = Instance.new("Frame")
                local dW = Instance.new("Frame")
                local cC = Instance.new("UICorner")
                local dX = Instance.new("TextLabel")
                local dY = Instance.new("TextButton")
                dV.Name = aY .. "dot"
                dV.Parent = aM
                dV.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dV.BackgroundTransparency = 1.000
                dV.Position = UDim2.new(0, 0, 0.300000012, 0)
                dV.Size = UDim2.new(1, 0, 0, 25)
                dW.Name = "ButtonBG"
                dW.Parent = dV
                dW.AnchorPoint = Vector2.new(0.5, 0.5)
                dW.Position = UDim2.new(0.5, 0, 0.5, 0)
                dW.Size = UDim2.new(1, -10, 1, 0)
                dW.BackgroundColor3 = getgenv().UIColor["Button Color"]
                table.insert(
                    c["Button Color"],
                    function()
                        dW.BackgroundColor3 = getgenv().UIColor["Button Color"]
                    end
                )
                dW.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        dW.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cC.CornerRadius = UDim.new(0, 4)
                cC.Name = "ButtonCorner"
                cC.Parent = dW
                dX.Name = "TextColor"
                dX.Parent = dW
                dX.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dX.BackgroundTransparency = 1.000
                dX.Position = UDim2.new(0, 10, 0, 0)
                dX.Size = UDim2.new(1, -10, 1, 0)
                dX.Font = Enum.Font.GothamBlack
                dX.Text = aY
                dX.TextSize = 14.000
                dX.TextXAlignment = Enum.TextXAlignment.Left
                dX.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        dX.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                dY.Name = "Button"
                dY.Parent = dW
                dY.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dY.BackgroundTransparency = 1.000
                dY.Size = UDim2.new(1, 0, 1, 0)
                dY.Font = Enum.Font.SourceSans
                dY.Text = ""
                dY.TextColor3 = Color3.fromRGB(0, 0, 0)
                dY.TextSize = 14.000
                dY.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                dY.MouseButton1Down:Connect(
                    function()
                        cN()
                    end
                )
            end
            function dJ.CreateLabel(H)
                local aY = tostring(H.Title)
                local dZ = Instance.new("Frame")
                local d_ = Instance.new("Frame")
                local e0 = Instance.new("UICorner")
                local e1 = Instance.new("TextLabel")
                dZ.Name = "LabelFrame"
                dZ.Parent = aM
                dZ.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                dZ.BackgroundTransparency = 1.000
                dZ.Position = UDim2.new(0, 0, 0, 0)
                dZ.Size = UDim2.new(1, 0, 0, 0)
                dZ.AutomaticSize = Enum.AutomaticSize.Y
                d_.Name = "LabelBG"
                d_.Parent = dZ
                d_.AnchorPoint = Vector2.new(0.5, 0)
                d_.Position = UDim2.new(0.5, 0, 0, 0)
                d_.Size = UDim2.new(1, -10, 0, -10)
                d_.BackgroundColor3 = getgenv().UIColor["Label Color"]
                d_.AutomaticSize = Enum.AutomaticSize.Y
                table.insert(
                    c["Label Color"],
                    function()
                        d_.BackgroundColor3 = getgenv().UIColor["Label Color"]
                    end
                )
                d_.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        d_.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                e0.CornerRadius = UDim.new(0, 4)
                e0.Name = "LabelCorner"
                e0.Parent = d_
                e1.Name = "TextColor"
                e1.Parent = d_
                e1.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                e1.BackgroundTransparency = 1.000
                e1.Position = UDim2.new(0, 10, 0, 3)
                e1.Size = UDim2.new(1, -20, 1, 0)
                e1.Font = Enum.Font.GothamBlack
                e1.Text = aY
                e1.TextSize = 14.000
                e1.TextXAlignment = Enum.TextXAlignment.Left
                e1.AutomaticSize = Enum.AutomaticSize.Y
                e1.TextWrapped = true
                e1.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        e1.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                local e2 = {}
                function e2.SetText(e3)
                    e1.Text = e3
                end
                function e2.SetColor(g)
                    e1.TextColor3 = g
                end
                return e2
            end
            function dJ.CreateDropdown(H, cN)
                local aY = tostring(H.Title)
                local e4 = H.List
                local e5 = H.Search or false
                local e6 = H.Selected or false
                local aZ = H.Default
                local cN = cN or function()
                    end
                local e7 = Instance.new("Frame")
                local e8 = Instance.new("Frame")
                local e9 = Instance.new("UICorner")
                local ea = Instance.new("Frame")
                local M = Instance.new("UICorner")
                local eb = Instance.new("ImageLabel")
                local ec = Instance.new("TextButton")
                local ed = Instance.new("Frame")
                local ee = Instance.new("ScrollingFrame")
                local ef = Instance.new("Frame")
                local eg = Instance.new("UIListLayout")
                local eh
                if e5 then
                    eh = Instance.new("TextBox")
                    ec.Visible = false
                else
                    eh = Instance.new("TextLabel")
                end
                e7.Name = aY .. "DropdownFrame"
                e7.Parent = aM
                e7.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                e7.BackgroundTransparency = 1.000
                e7.Position = UDim2.new(0, 0, 0.473684222, 0)
                e7.Size = UDim2.new(1, 0, 0, 25)
                e8.Name = "Background1"
                e8.Parent = e7
                e8.AnchorPoint = Vector2.new(0.5, 0.5)
                e8.Position = UDim2.new(0.5, 0, 0.5, 0)
                e8.Size = UDim2.new(1, -10, 1, 0)
                e8.ClipsDescendants = true
                e8.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        e8.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                e8.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        e8.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                e9.CornerRadius = UDim.new(0, 4)
                e9.Name = "Dropdowncorner"
                e9.Parent = e8
                ea.Name = "Background2"
                ea.Parent = e8
                ea.Size = UDim2.new(1, 0, 0, 25)
                ea.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        ea.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                ea.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        ea.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                M.CornerRadius = UDim.new(0, 4)
                M.Parent = ea
                eh.Name = "TextColorPlaceholder"
                eh.Parent = ea
                eh.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                eh.BackgroundTransparency = 1.000
                eh.Position = UDim2.new(0, 10, 0, 0)
                eh.Size = UDim2.new(1, -40, 1, 0)
                eh.Font = Enum.Font.GothamBlack
                eh.Text = ""
                eh.TextSize = 14.000
                eh.TextXAlignment = Enum.TextXAlignment.Left
                eh.ClipsDescendants = true
                local ei = Instance.new("IntValue", eh)
                ei.Value = -1
                if aZ and table.find(e4, aZ) then
                    ei.Value = table.find(e4, aZ)
                end
                if not e6 then
                    if e5 then
                        eh.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                        eh.PlaceholderText = aY .. ": " .. tostring(aZ)
                        table.insert(
                            c["Placeholder Text Color"],
                            function()
                                eh.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                            end
                        )
                    else
                        eh.Text = aY .. ": " .. tostring(aZ)
                    end
                else
                    if e5 then
                        eh.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                        eh.PlaceholderText = aY .. ": " .. tostring(aZ)
                        table.insert(
                            c["Placeholder Text Color"],
                            function()
                                eh.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                            end
                        )
                    else
                        eh.Text = aY .. ": " .. tostring(aZ)
                    end
                end
                eh.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        eh.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                eb.Name = "ImgDrop"
                eb.Parent = ea
                eb.AnchorPoint = Vector2.new(1, 0.5)
                eb.BackgroundTransparency = 1.000
                eb.BorderColor3 = Color3.fromRGB(27, 42, 53)
                eb.Position = UDim2.new(1, -6, 0.5, 0)
                eb.Size = UDim2.new(0, 15, 0, 15)
                eb.Image = "rbxassetid://6954383209"
                eb.ImageColor3 = getgenv().UIColor["Dropdown Icon Color"]
                table.insert(
                    c["Dropdown Icon Color"],
                    function()
                        eb.ImageColor3 = getgenv().UIColor["Dropdown Icon Color"]
                    end
                )
                ec.Name = "DropdownButton"
                ec.Parent = ea
                ec.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                ec.BackgroundTransparency = 1.000
                ec.Size = UDim2.new(1, 0, 1, 0)
                ec.Font = Enum.Font.GothamBold
                ec.Text = ""
                ec.TextColor3 = Color3.fromRGB(230, 230, 230)
                ec.TextSize = 14.000
                ed.Name = "Dropdownlisttt"
                ed.Parent = e8
                ed.BackgroundTransparency = 1.000
                ed.BorderSizePixel = 0
                ed.Position = UDim2.new(0, 0, 0, 25)
                ed.Size = UDim2.new(1, 0, 0, 25)
                ed.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                ee.Name = "DropdownScroll"
                ee.Parent = ed
                ee.Active = true
                ee.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                ee.BackgroundTransparency = 1.000
                ee.BorderSizePixel = 0
                ee.Size = UDim2.new(1, 0, 1, 0)
                ee.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
                ee.CanvasSize = UDim2.new(0, 0, 0, 0)
                ee.ScrollBarThickness = 5
                ee.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
                ef.Name = "ScrollContainer"
                ef.Parent = ee
                ef.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                ef.BackgroundTransparency = 1.000
                ef.Position = UDim2.new(0, 5, 0, 5)
                ef.Size = UDim2.new(1, -15, 1, -5)
                eg.Name = "ScrollContainerList"
                eg.Parent = ef
                eg.SortOrder = Enum.SortOrder.LayoutOrder
                eg:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(
                    function()
                        ee.CanvasSize = UDim2.new(0, 0, 0, 10 + eg.AbsoluteContentSize.Y + 5)
                    end
                )
                local ej = false
                local ek = {}
                local el = {}
                local function em()
                    for a in pairs(ek) do
                        ek[a] = nil
                    end
                    for en, eo in pairs(ef:GetChildren()) do
                        if not eo:IsA("UIListLayout") and not eo:IsA("UIPadding") and not eo:IsA("UIGridLayout") then
                            eo.Visible = false
                        end
                    end
                    eh.Text = string.lower(eh.Text)
                end
                local function ep()
                    local eq = {}
                    for a, v in pairs(el) do
                        if string.find(v, eh.Text) then
                            table.insert(ek, v)
                        end
                    end
                    for n, B in pairs(ef:GetChildren()) do
                        for er, es in pairs(ek) do
                            if es == B.Name then
                                B.Visible = true
                            end
                        end
                    end
                end
                local function et()
                    for a, v in next, ef:GetChildren() do
                        if v:IsA("Frame") then
                            v:Destroy()
                        end
                    end
                end
                local eu = e4
                local function ev()
                    et()
                    el = {}
                    for a, v in pairs(eu) do
                        if not e6 then
                            table.insert(el, string.lower(v))
                        else
                            table.insert(el, string.lower(a))
                        end
                    end
                    if not e6 then
                        for a, v in pairs(eu) do
                            local ew = Instance.new("Frame")
                            local ex = Instance.new("UICorner")
                            local ds = Instance.new("Frame")
                            local dt = Instance.new("Frame")
                            local du = Instance.new("UICorner")
                            local ey = Instance.new("Frame")
                            local ez = Instance.new("TextButton")
                            ew.Name = string.lower(v)
                            ew.Parent = ef
                            ew.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ew.BackgroundTransparency = 1.000
                            ew.Size = UDim2.new(1, 0, 0, 25)
                            ex.CornerRadius = UDim.new(0, 4)
                            ex.Name = "DropvalCorner"
                            ex.Parent = ew
                            ds.Name = "Line"
                            ds.Parent = ew
                            ds.AnchorPoint = Vector2.new(0, 0.5)
                            ds.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ds.BackgroundTransparency = 1.000
                            ds.Position = UDim2.new(0, 0, 0.5, 0)
                            ds.Size = UDim2.new(0, 14, 1, 0)
                            dt.Name = "InLine"
                            dt.Parent = ds
                            dt.AnchorPoint = Vector2.new(0.5, 0.5)
                            dt.BorderSizePixel = 0
                            dt.Position = UDim2.new(0.5, 0, 0.5, 0)
                            dt.Size = UDim2.new(1, -10, 1, -10)
                            dt.BackgroundTransparency = 1
                            dt.BackgroundColor3 = getgenv().UIColor["Dropdown Selected Color"]
                            table.insert(
                                c["Dropdown Selected Color"],
                                function()
                                    dt.BackgroundColor3 = getgenv().UIColor["Dropdown Selected Color"]
                                end
                            )
                            du.Name = "LineCorner"
                            du.Parent = dt
                            ey.Name = "Dropvalcontainer"
                            ey.Parent = ew
                            ey.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ey.BackgroundTransparency = 1.000
                            ey.Position = UDim2.new(0, 15, 0, 0)
                            ey.Size = UDim2.new(1, -15, 1, 0)
                            ez.Name = "TextColor"
                            ez.Parent = ey
                            ez.Active = false
                            ez.BackgroundTransparency = 1.000
                            ez.Selectable = false
                            ez.Size = UDim2.new(1, 0, 1, 0)
                            ez.Font = Enum.Font.GothamBold
                            ez.Text = v
                            ez.TextSize = 14.000
                            ez.TextWrapped = true
                            ez.TextXAlignment = Enum.TextXAlignment.Left
                            ez.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ez.TextColor3 = getgenv().UIColor["Text Color"]
                            table.insert(
                                c["Text Color"],
                                function()
                                    ez.TextColor3 = getgenv().UIColor["Text Color"]
                                end
                            )
                            if e5 then
                                if ei.Value == a then
                                    dt.BackgroundTransparency = 0
                                end
                            else
                                if ei.Value == a then
                                    dt.BackgroundTransparency = 0
                                end
                            end
                            ez.MouseButton1Click:Connect(
                                function()
                                    if e5 then
                                        eh.PlaceholderText = aY .. ": " .. v
                                        ei.Value = a
                                    else
                                        eh.Text = aY .. ": " .. v
                                        ei.Value = a
                                    end
                                    ev()
                                    if cN then
                                        cN(v, a)
                                    end
                                end
                            )
                            ez.MouseButton1Click:Connect(
                                function()
                                    u.ButtonEffect()
                                end
                            )
                        end
                    else
                        for a, v in pairs(eu) do
                            local eA = v and 0 or 1
                            local ew = Instance.new("Frame")
                            local ex = Instance.new("UICorner")
                            local ds = Instance.new("Frame")
                            local dt = Instance.new("Frame")
                            local du = Instance.new("UICorner")
                            local ey = Instance.new("Frame")
                            local ez = Instance.new("TextButton")
                            ew.Name = string.lower(a)
                            ew.Parent = ef
                            ew.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ew.BackgroundTransparency = 1.000
                            ew.Size = UDim2.new(1, 0, 0, 25)
                            ex.CornerRadius = UDim.new(0, 4)
                            ex.Name = "DropvalCorner"
                            ex.Parent = ew
                            ds.Name = "Line"
                            ds.Parent = ew
                            ds.AnchorPoint = Vector2.new(0, 0.5)
                            ds.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ds.BackgroundTransparency = 1
                            ds.Position = UDim2.new(0, 0, 0.5, 0)
                            ds.Size = UDim2.new(0, 14, 1, 0)
                            dt.Name = "InLine"
                            dt.Parent = ds
                            dt.AnchorPoint = Vector2.new(0.5, 0.5)
                            dt.BorderSizePixel = 0
                            dt.Position = UDim2.new(0.5, 0, 0.5, 0)
                            dt.Size = UDim2.new(1, -10, 1, -10)
                            dt.BackgroundTransparency = eA
                            dt.BackgroundColor3 = getgenv().UIColor["Dropdown Selected Color"]
                            table.insert(
                                c["Dropdown Selected Color"],
                                function()
                                    dt.BackgroundColor3 = getgenv().UIColor["Dropdown Selected Color"]
                                end
                            )
                            du.Name = "LineCorner"
                            du.Parent = dt
                            ey.Name = "Dropvalcontainer"
                            ey.Parent = ew
                            ey.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ey.BackgroundTransparency = 1.000
                            ey.Position = UDim2.new(0, 15, 0, 0)
                            ey.Size = UDim2.new(1, -15, 1, 0)
                            ez.Name = "TextColor"
                            ez.Parent = ey
                            ez.Active = false
                            ez.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                            ez.BackgroundTransparency = 1.000
                            ez.Selectable = false
                            ez.Size = UDim2.new(1, 0, 1, 0)
                            ez.Font = Enum.Font.GothamBold
                            ez.Text = a
                            ez.TextSize = 14.000
                            ez.TextWrapped = true
                            ez.TextXAlignment = Enum.TextXAlignment.Left
                            ez.TextColor3 = getgenv().UIColor["Text Color"]
                            table.insert(
                                c["Text Color"],
                                function()
                                    ez.TextColor3 = getgenv().UIColor["Text Color"]
                                end
                            )
                            ez.MouseButton1Click:Connect(
                                function()
                                    u.ButtonEffect()
                                end
                            )
                            ez.MouseButton1Click:Connect(
                                function()
                                    v = not v
                                    local eA = v and 0 or 1
                                    w:Create(
                                        dt,
                                        TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                                        {BackgroundTransparency = eA}
                                    ):Play()
                                    if cN then
                                        cN(a, v)
                                        eu[a] = v
                                    end
                                end
                            )
                        end
                    end
                end
                if e5 then
                    eh.Changed:Connect(
                        function()
                            em()
                            ep()
                        end
                    )
                end
                if typeof(aZ) ~= "table" then
                    cN(aZ)
                    if e5 then
                        eh.PlaceholderText = aY .. ": " .. tostring(aZ)
                    else
                        eh.Text = aY .. ": " .. tostring(aZ)
                    end
                elseif e6 then
                    for a, v in next, aZ do
                        eu[a] = v
                        cN(a, v)
                    end
                    eh.Text = ""
                    eh.PlaceholderText = aY .. ": "
                end
                ec.MouseButton1Click:Connect(
                    function()
                        ev()
                        ej = not ej
                        local eB = ej and UDim2.new(1, 0, 0, 170) or UDim2.new(1, 0, 0, 0)
                        local eC = ej and UDim2.new(1, 0, 0, 200) or UDim2.new(1, 0, 0, 25)
                        local eD = ej and 90 or 0
                        w:Create(ed, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eB}):Play()
                        w:Create(e7, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eC}):Play()
                        w:Create(eb, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Rotation = eD}):Play(

                        )
                    end
                )
                ec.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                if e5 then
                    eh.Focused:Connect(
                        function()
                            ev()
                            ej = not ej
                            local eB = ej and UDim2.new(1, 0, 0, 170) or UDim2.new(1, 0, 0, 0)
                            local eC = ej and UDim2.new(1, 0, 0, 200) or UDim2.new(1, 0, 0, 25)
                            local eD = ej and 90 or 0
                            w:Create(ed, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eB}):Play(

                            )
                            w:Create(e7, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eC}):Play(

                            )
                            w:Create(eb, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Rotation = eD}):Play(

                            )
                        end
                    )
                    eh.Focused:Connect(
                        function()
                            u.ButtonEffect()
                        end
                    )
                end
                local eE = {rf = ev}
                function eE:ClearText()
                    if not e6 then
                        if e5 then
                            eh.PlaceholderText = aY .. ": "
                        else
                            eh.Text = aY .. ": "
                        end
                    else
                        eh.Text = aY .. ": "
                    end
                end
                function eE:GetNewList(e4)
                    ev()
                    ej = false
                    local eB = ej and UDim2.new(1, 0, 0, 170) or UDim2.new(1, 0, 0, 0)
                    local eC = ej and UDim2.new(1, 0, 0, 200) or UDim2.new(1, 0, 0, 25)
                    local eD = ej and 90 or 0
                    w:Create(ed, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eB}):Play()
                    w:Create(e7, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Size = eC}):Play()
                    w:Create(eb, TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]), {Rotation = eD}):Play()
                    eu = {}
                    eu = e4
                    for a, v in next, eu do
                        if e6 then
                            cN(a, v)
                        end
                    end
                end
                return eE
            end
            function dJ.CreateBind(H, cN)
                local cx = tostring(H.Title) or ""
                local eF = H.Key
                local aZ = H.Default or H.Key
                local a_ = tostring(aZ):match("UserInputType") and "UserInputType" or "KeyCode"
                local cN = cN or function()
                    end
                eF = tostring(eF):gsub("Enum.UserInputType.", "")
                eF = tostring(eF):gsub("Enum.KeyCode.", "")
                local eG = Instance.new("Frame")
                local eH = Instance.new("UICorner")
                local eI = Instance.new("Frame")
                local cC = Instance.new("UICorner")
                local eJ = Instance.new("TextLabel")
                local dY = Instance.new("TextButton")
                local eK = Instance.new("Frame")
                local cF = Instance.new("UICorner")
                local eL = Instance.new("TextButton")
                eG.Name = cx .. "bguvl"
                eG.Parent = aM
                eG.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                eG.BackgroundTransparency = 1.000
                eG.Position = UDim2.new(0, 0, 0.208333328, 0)
                eG.Size = UDim2.new(1, 0, 0, 35)
                eH.CornerRadius = UDim.new(0, 4)
                eH.Name = "BindCorner"
                eH.Parent = eG
                eI.Name = "Background1"
                eI.Parent = eG
                eI.AnchorPoint = Vector2.new(0.5, 0.5)
                eI.Position = UDim2.new(0.5, 0, 0.5, 0)
                eI.Size = UDim2.new(1, -10, 1, 0)
                eI.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        eI.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                eI.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        eI.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cC.CornerRadius = UDim.new(0, 4)
                cC.Name = "ButtonCorner"
                cC.Parent = eI
                eJ.Name = "TextColor"
                eJ.Parent = eI
                eJ.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                eJ.BackgroundTransparency = 1.000
                eJ.Position = UDim2.new(0, 10, 0, 0)
                eJ.Size = UDim2.new(1, -10, 1, 0)
                eJ.Font = Enum.Font.GothamBlack
                eJ.Text = cx
                eJ.TextSize = 14.000
                eJ.TextXAlignment = Enum.TextXAlignment.Left
                eJ.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        eJ.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                eK.Name = "Background2"
                eK.Parent = eI
                eK.AnchorPoint = Vector2.new(1, 0.5)
                eK.Position = UDim2.new(1, -5, 0.5, 0)
                eK.Size = UDim2.new(0, 150, 0, 25)
                eK.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        eK.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                cF.CornerRadius = UDim.new(0, 4)
                cF.Name = "ButtonCorner"
                cF.Parent = eK
                eL.Name = "Bindkey"
                eL.Parent = eK
                eL.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                eL.BackgroundTransparency = 1.000
                eL.Size = UDim2.new(1, 0, 1, 0)
                eL.Font = Enum.Font.GothamBold
                eL.Text = tostring(aZ):gsub("Enum.KeyCode.", "")
                eL.TextSize = 14.000
                eL.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        eL.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                local eM = {
                    [Enum.UserInputType.MouseButton1] = "Mouse1",
                    [Enum.UserInputType.MouseButton2] = "Mouse2",
                    [Enum.UserInputType.MouseButton3] = "Mouse3"
                }
                eL.MouseButton1Click:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                eL.MouseButton1Click:Connect(
                    function()
                        local eN
                        eL.Text = "..."
                        eN =
                            game:GetService("UserInputService").InputBegan:Connect(
                            function(a)
                                if eM[a.UserInputType] then
                                    eL.Text = eM[a.UserInputType]
                                    spawn(
                                        function()
                                            wait(0.1)
                                            aZ = a.UserInputType
                                            a_ = "UserInputType"
                                        end
                                    )
                                elseif a.KeyCode ~= Enum.KeyCode.Unknown then
                                    eL.Text = tostring(a.KeyCode):gsub("Enum.KeyCode.", "")
                                    spawn(
                                        function()
                                            wait(0.1)
                                            aZ = a.KeyCode
                                            a_ = "KeyCode"
                                        end
                                    )
                                end
                                eN:Disconnect()
                            end
                        )
                    end
                )
                game:GetService("UserInputService").InputBegan:Connect(
                    function(a)
                        if aZ == a.UserInputType or aZ == a.KeyCode then
                            cN(aZ)
                        end
                    end
                )
            end
            function dJ.CreateBox(H, cN)
                local cx = tostring(H.Title) or ""
                local cy = tostring(H.Placeholder) or ""
                local aZ = H.Default or false
                local eO = H.Number or false
                local cN = cN or function()
                    end
                local cz = Instance.new("Frame")
                local cA = Instance.new("UICorner")
                local cB = Instance.new("Frame")
                local cC = Instance.new("UICorner")
                local cD = Instance.new("TextLabel")
                local cE = Instance.new("Frame")
                local cF = Instance.new("UICorner")
                local eP = Instance.new("TextBox")
                local cH = Instance.new("Frame")
                local M = Instance.new("UICorner")
                cz.Name = "BoxFrame"
                cz.Parent = aM
                cz.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                cz.BackgroundTransparency = 1.000
                cz.Position = UDim2.new(0, 0, 0.208333328, 0)
                cz.Size = UDim2.new(1, 0, 0, 60)
                cA.CornerRadius = UDim.new(0, 4)
                cA.Name = "BoxCorner"
                cA.Parent = cz
                cB.Name = "Background1"
                cB.Parent = cz
                cB.AnchorPoint = Vector2.new(0.5, 0.5)
                cB.Position = UDim2.new(0.5, 0, 0.5, 0)
                cB.Size = UDim2.new(1, -10, 1, 0)
                cB.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        cB.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                cB.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        cB.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cC.CornerRadius = UDim.new(0, 4)
                cC.Name = "ButtonCorner"
                cC.Parent = cB
                cD.Name = "TextColor"
                cD.Parent = cB
                cD.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                cD.BackgroundTransparency = 1.000
                cD.Position = UDim2.new(0, 10, 0, 0)
                cD.Size = UDim2.new(1, -10, 0.5, 0)
                cD.Font = Enum.Font.GothamBlack
                cD.Text = cx
                cD.TextSize = 14.000
                cD.TextXAlignment = Enum.TextXAlignment.Left
                cD.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        cD.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cE.Name = "Background2"
                cE.Parent = cB
                cE.AnchorPoint = Vector2.new(1, 0.5)
                cE.ClipsDescendants = true
                cE.Position = UDim2.new(1, -5, 0, 40)
                cE.Size = UDim2.new(1, -10, 0, 25)
                cE.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        cE.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                cF.CornerRadius = UDim.new(0, 4)
                cF.Name = "ButtonCorner"
                cF.Parent = cE
                eP.Name = "TextColorPlaceholder"
                eP.Parent = cE
                eP.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                eP.BackgroundTransparency = 1.000
                eP.Position = UDim2.new(0, 5, 0, 0)
                eP.Size = UDim2.new(1, -5, 1, 0)
                eP.Font = Enum.Font.GothamBold
                eP.PlaceholderText = cy
                eP.Text = ""
                eP.TextSize = 14.000
                eP.TextXAlignment = Enum.TextXAlignment.Left
                eP.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                eP.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Placeholder Text Color"],
                    function()
                        eP.PlaceholderColor3 = getgenv().UIColor["Placeholder Text Color"]
                    end
                )
                table.insert(
                    c["Text Color"],
                    function()
                        eP.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cH.Name = "TextNSBoxLineeeee"
                cH.Parent = cE
                cH.BackgroundTransparency = 1.000
                cH.Position = UDim2.new(0, 0, 1, -2)
                cH.Size = UDim2.new(1, 0, 0, 6)
                cH.BackgroundColor3 = getgenv().UIColor["Box Highlight Color"]
                table.insert(
                    c["Box Highlight Color"],
                    function()
                        cH.BackgroundColor3 = getgenv().UIColor["Box Highlight Color"]
                    end
                )
                M.CornerRadius = UDim.new(1, 0)
                M.Parent = cH
                eP.Focused:Connect(
                    function()
                        w:Create(
                            cH,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundTransparency = 0}
                        ):Play()
                    end
                )
                eP.Focused:Connect(
                    function()
                        u.ButtonEffect()
                    end
                )
                if eO then
                    eP:GetPropertyChangedSignal("Text"):Connect(
                        function()
                            if tonumber(eP.Text) then
                            else
                                eP.PlaceholderText = cy
                                eP.Text = ""
                            end
                        end
                    )
                end
                eP.FocusLost:Connect(
                    function()
                        w:Create(
                            cH,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundTransparency = 1}
                        ):Play()
                        if eP.Text ~= "" then
                            cN(eP.Text)
                        end
                    end
                )
                local cI = {}
                if aZ then
                    eP.Text = aZ
                    cN(aZ)
                end
                function cI.SetValue(r)
                    eP.Text = r
                    cN(r)
                end
                return cI
            end
            function dJ.CreateSlider(H, cN)
                local cx = tostring(H.Title) or ""
                local cJ = tonumber(H.Min) or 0
                local cK = tonumber(H.Max) or 100
                local cL = H.Precise or false
                local cM = tonumber(H.Default) or 0
                local cN = cN or function()
                    end
                local cO = 400
                local cN = cN or function()
                    end
                local cP = Instance.new("Frame")
                local cQ = Instance.new("UICorner")
                local cR = Instance.new("Frame")
                local cS = Instance.new("UICorner")
                local cT = Instance.new("TextLabel")
                local cU = Instance.new("Frame")
                local cV = Instance.new("TextButton")
                local cW = Instance.new("UICorner")
                local cX = Instance.new("Frame")
                local cY = Instance.new("UICorner")
                local cZ = Instance.new("Frame")
                local c_ = Instance.new("UICorner")
                local d0 = Instance.new("TextBox")
                cP.Name = cx .. "buda"
                cP.Parent = aM
                cP.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
                cP.BackgroundTransparency = 1.000
                cP.Position = UDim2.new(0, 0, 0.208333328, 0)
                cP.Size = UDim2.new(1, 0, 0, 50)
                cQ.CornerRadius = UDim.new(0, 4)
                cQ.Name = "SliderCorner"
                cQ.Parent = cP
                cR.Name = "Background1"
                cR.Parent = cP
                cR.AnchorPoint = Vector2.new(0.5, 0.5)
                cR.Position = UDim2.new(0.5, 0, 0.5, 0)
                cR.Size = UDim2.new(1, -10, 1, 0)
                cR.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                table.insert(
                    c["Background 1 Color"],
                    function()
                        cR.BackgroundColor3 = getgenv().UIColor["Background 1 Color"]
                    end
                )
                cR.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                table.insert(
                    c["Background 1 Transparency"],
                    function()
                        cR.BackgroundTransparency = getgenv().UIColor["Background 1 Transparency"]
                    end
                )
                cS.CornerRadius = UDim.new(0, 4)
                cS.Name = "SliderBGCorner"
                cS.Parent = cR
                cT.Name = "TextColor"
                cT.Parent = cR
                cT.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                cT.BackgroundTransparency = 1.000
                cT.Position = UDim2.new(0, 10, 0, 0)
                cT.Size = UDim2.new(1, -10, 0, 25)
                cT.Font = Enum.Font.GothamBlack
                cT.Text = cx
                cT.TextSize = 14.000
                cT.TextXAlignment = Enum.TextXAlignment.Left
                cT.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        cT.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cU.Name = "SliderBar"
                cU.Parent = cP
                cU.AnchorPoint = Vector2.new(.5, 0.5)
                cU.Position = UDim2.new(.5, 0, 0.5, 14)
                cU.Size = UDim2.new(0, 400, 0, 6)
                cU.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        cU.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                cV.Name = "SliderButton "
                cV.Parent = cU
                cV.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                cV.BackgroundTransparency = 1.000
                cV.Size = UDim2.new(1, 0, 1, 0)
                cV.Font = Enum.Font.GothamBold
                cV.Text = ""
                cV.TextColor3 = Color3.fromRGB(230, 230, 230)
                cV.TextSize = 14.000
                cW.CornerRadius = UDim.new(1, 0)
                cW.Name = "SliderBarCorner"
                cW.Parent = cU
                cX.Name = "Bar"
                cX.BorderSizePixel = 0
                cX.Parent = cU
                cX.Size = UDim2.new(0, 0, 1, 0)
                cX.BackgroundColor3 = getgenv().UIColor["Slider Line Color"]
                table.insert(
                    c["Slider Line Color"],
                    function()
                        cX.BackgroundColor3 = getgenv().UIColor["Slider Line Color"]
                    end
                )
                cY.CornerRadius = UDim.new(1, 0)
                cY.Name = "BarCorner"
                cY.Parent = cX
                cZ.Name = "Background2"
                cZ.Parent = cP
                cZ.AnchorPoint = Vector2.new(1, 0)
                cZ.Position = UDim2.new(1, -10, 0, 5)
                cZ.Size = UDim2.new(0, 150, 0, 25)
                cZ.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                table.insert(
                    c["Background 2 Color"],
                    function()
                        cZ.BackgroundColor3 = getgenv().UIColor["Background 2 Color"]
                    end
                )
                c_.CornerRadius = UDim.new(0, 4)
                c_.Name = "Sliderbox"
                c_.Parent = cZ
                d0.Name = "TextColor"
                d0.Parent = cZ
                d0.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
                d0.BackgroundTransparency = 1.000
                d0.Size = UDim2.new(1, 0, 1, 0)
                d0.Font = Enum.Font.GothamBold
                d0.Text = ""
                d0.TextSize = 14.000
                d0.TextColor3 = getgenv().UIColor["Text Color"]
                table.insert(
                    c["Text Color"],
                    function()
                        d0.TextColor3 = getgenv().UIColor["Text Color"]
                    end
                )
                cV.MouseEnter:Connect(
                    function()
                        w:Create(
                            cX,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundColor3 = getgenv().UIColor["Slider Highlight Color"]}
                        ):Play()
                    end
                )
                cV.MouseLeave:Connect(
                    function()
                        w:Create(
                            cX,
                            TweenInfo.new(getgenv().UIColor["Tween Animation 2 Speed"]),
                            {BackgroundColor3 = getgenv().UIColor["Slider Line Color"]}
                        ):Play()
                    end
                )
                local y = game.Players.LocalPlayer:GetMouse()
                if cM then
                    if cM <= cJ then
                        cM = cJ
                    elseif cM >= cK then
                        cM = cK
                    end
                    cX.Size = UDim2.new(1 - (cK - cM) / (cK - cJ), 0, 0, 6)
                    d0.Text = cM
                    cN(cM)
                end
                cV.MouseButton1Down:Connect(
                    function()
                        local d1 =
                            cL and
                            tonumber(
                                string.format(
                                    "%.1f",
                                    (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                )
                            ) or
                            math.floor((tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ))
                        pcall(
                            function()
                                cN(d1)
                                d0.Text = d1
                            end
                        )
                        cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                        moveconnection =
                            y.Move:Connect(
                            function()
                                local d1 =
                                    cL and
                                    tonumber(
                                        string.format(
                                            "%.1f",
                                            (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                        )
                                    ) or
                                    math.floor((tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ))
                                pcall(
                                    function()
                                        cN(d1)
                                        d0.Text = d1
                                    end
                                )
                                cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                            end
                        )
                        releaseconnection =
                            x.InputEnded:Connect(
                            function(d2)
                                if d2.UserInputType == Enum.UserInputType.MouseButton1 then
                                    local d1 =
                                        cL and
                                        tonumber(
                                            string.format(
                                                "%.1f",
                                                (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                            )
                                        ) or
                                        math.floor(
                                            (tonumber(cK) - tonumber(cJ)) / cO * cX.AbsoluteSize.X + tonumber(cJ)
                                        )
                                    pcall(
                                        function()
                                            cN(d1)
                                            d0.Text = d1
                                        end
                                    )
                                    cX.Size = UDim2.new(0, math.clamp(y.X - cX.AbsolutePosition.X, 0, cO), 0, 6)
                                    moveconnection:Disconnect()
                                    releaseconnection:Disconnect()
                                end
                            end
                        )
                    end
                )
                local function d3(r)
                    if tonumber(r) <= cJ then
                        cX.Size = UDim2.new(0, 0 * cO, 0, 6)
                        d0.Text = cJ
                        cN(tonumber(cJ))
                    elseif tonumber(r) >= cK then
                        cX.Size = UDim2.new(0, cK / cK * cO, 0, 6)
                        d0.Text = cK
                        cN(tonumber(cK))
                    else
                        cX.Size = UDim2.new(1 - (cK - r) / (cK - cJ), 0, 0, 6)
                        cN(tonumber(r))
                    end
                end
                d0.FocusLost:Connect(
                    function()
                        d3(d0.Text)
                    end
                )
                local d4 = {}
                function d4.SetValue(r)
                    d3(r)
                end
                return d4
            end
            return dJ
        end
        return dI
    end
    return dj
end
return t end
print("\nTai sao Vo Hoang lai nang den muc vay\nWhy Vo Hoang can be that tard")
print("Sucvat123")
local rnd = tostring(math.random(1,100000))
local Library = GetUi()

-- (function() 
--     local concac

--     if isfile("uilib.lua") then 
--         concac = readfile("uilib.lua")
--         Library=loadstring(concac)()
--         --print(Library)
--     else
--         concac = game:HttpGet("https://raw.githubusercontent.com/7bgqRy0CC2wCjblo9W4kmWBejs72uKCNqI7XqUL/SeaUILib/main/UI/Logo")
--     end
--     if not Library then 
--         Library =loadstring(syn.crypt.decrypt(concac,"cac"))() end
-- end)()
local keylist = {"af298fe2fe0361c","e69327320bfcb7e","66036fb2f36e983","f27c0d2a3bee5a6","","ad4f5fc1ec8dd0a","2341aff65def585"} --,"d96d10a1b806168"
local key = getgenv().Key or ""
--setclipboard(syn.crypt.decrypt(concac,"cac"))
--local Library=loadstring(concac)()

wait()
local FieldFarmPos = {
    -- SunflowerField = {
    --     Listpos = {},
    --     Range = {}
    -- }
}
local Cache = {}
local plr = game.Players.LocalPlayer
local Settings = {mothaiba=true}

function formatNumber(v)
    return tostring(v):reverse():gsub("%d%d%d", "%1,"):reverse():gsub("^,", "")
end
function vToK(tabl)
    local out = {}
    for k, v in pairs(tabl) do
        out[v] = k
    end
    return out
end
function RemoveVal(tb,val) 
    for k,v in pairs(tb) do 
        if v==val then 
            table.remove(tb,k)
            break;
        end    
    end
end
function DienTichTamGiac(x,y,z)
    x=Vector3.new(x.X,0,x.Z)
    y=Vector3.new(y.X,0,y.Z)
    z=Vector3.new(z.X,0,z.Z)
    
    local a = (x-y).magnitude
    local b = (y-z).magnitude
    local c = (x-z).magnitude
    local cv = a+b+c
    local p = cv/2
    local S =(p*(p-a)*(p-b)*(p-c))
    return S
end 

-- function IsInTriagule(Point,a,b,c) 
--     print(DienTichTamGiac(a,b,Point)+DienTichTamGiac(a,Point,c) + DienTichTamGiac(Point,b,c)-DienTichTamGiac(a,b,c))
--     return DienTichTamGiac(a,b,Point)+DienTichTamGiac(a,Point,c) + DienTichTamGiac(Point,b,c) == DienTichTamGiac(a,b,c)
-- end
function IsInTriagule(point, a,b,c)
    a=Vector3.new(a.X,0,a.Z)
    b=Vector3.new(b.X,0,b.Z)
    c=Vector3.new(c.X,0,c.Z)
    local triangle = {a,b,c}
    local v0 = triangle[3] - triangle[1]
    local v1 = triangle[2] - triangle[1]
    local v2 = point - triangle[1]
  
    local dot00 = v0:Dot(v0)
    local dot01 = v0:Dot(v1)
    local dot02 = v0:Dot(v2)
    local dot11 = v1:Dot(v1)
    local dot12 = v1:Dot(v2)
  
    local invDenom = 1 / (dot00 * dot11 - dot01 * dot01)
    local u = (dot11 * dot02 - dot01 * dot12) * invDenom
    local v = (dot00 * dot12 - dot01 * dot02) * invDenom
  
    return (u >= 0) and (v >= 0) and (u + v < 1)
  end

function ToTrueFalse(tabl, f)
    local out = {}
    for k, v in pairs(tabl) do
        if f then
            out[k] = f
        else
            out[k] = false
        end
    end

    return out
end
function ToST(tabl, s)
    local out = {}
    for k, v in pairs(tabl) do
       out[k]=s
    end
    return out
end


repeat wait() until game:IsLoaded()
local plr = game.Players.LocalPlayer
repeat wait() until plr
repeat wait() until plr.Character
repeat wait() until plr.Character:FindFirstChild("HumanoidRootPart")
repeat wait() until plr.PlayerGui:FindFirstChild("ScreenGui")
repeat wait() until plr.PlayerGui:FindFirstChild("ScreenGui"):FindFirstChild("Menus")
repeat wait() until plr.PlayerGui:FindFirstChild("ScreenGui"):FindFirstChild("LoadingMessage")
repeat wait() until plr.PlayerGui:FindFirstChild("ScreenGui"):FindFirstChild("LoadingMessage").Visible==false
local connect
local funcwrap
local ret
local ListFunc = {}
local old
local connect2
old = hookmetamethod(game,"__index",function(...) 
    if checkcaller() then return old(...) end
    if not connect then 
        connect=Instance.new("IntValue")
        connect.Changed:Connect(function(val)
            if val==100 then 
                for k,v in pairs(ListFunc) do 
                    if not v.Done then 
                        spawn(function() 
                            local s,e = pcall(function() 
                                v.Res = k()
                            end)
                            if e then print(e) end
                            v.tvk = true
                            connect2.Value=100
                            connect2.Value=0
                        end)
                        v.Done=true
                    end
                end
            end 
        end)
    end
    return old(...)
end)
repeat wait() until connect
print("Connected")
function warpF2(f) 
    if not connect2 then 
        connect2=Instance.new("IntValue")
    end
    ListFunc[f] = {}


    connect.Value=100
    connect.Value=0
    
    while not ListFunc[f].tvk do 
        connect2.Changed:Wait()
    end
    local res = ListFunc[f].Res
    ListFunc[f] = nil
    return res
end
-- local old = require
-- local hash = {}
-- local require = function(x) 
--     if hash[x] then 
--         return hash[x]
--     end
--     hash[x] = warpF2(function() return old(x) end)
--     return hash[x]
-- end
local u1 = require(game.ReplicatedStorage.ClientStatCache);
local Killing

local name = plr.Name
function hup()
    local old
    old = hookmetamethod(game,"__namecall",function(...) 
        if checkcaller() then 
            if getnamecallmethod() == "WaitForChild" then 
                if plr.Character then 
                    local Self,Key,Time = ...
                    if Self == plr.Character then 
                        if plr.Character:FindFirstChild(Key) then 
                            return plr.Character:FindFirstChild(Key)
                        else
                            repeat wait() until plr.Character and plr.Character:FindFirstChild(Key)
                            return plr.Character:FindFirstChild(Key)
                        end
                    end
                end
            end
        end
        return old(...)
    end)

    local old
    old = hookmetamethod(game,"__index",function(...) 
        local self,key = ...
        if checkcaller() then 
            if tostring(self) == name and key == "HumanoidRootPart" then 
                return self:WaitForChild("HumanoidRootPart")
            end
        end
        return old(...)
    end)
end
hup()

local ListTileGrid = {}

function DisableGlider() 
    local uis = game:GetService("UserInputService")
    for k,v in pairs(getconnections(uis.JumpRequest)) do 
        v:Disable()    
    end
end
function EnableGlider() 
    local uis = game:GetService("UserInputService")
    for k,v in pairs(getconnections(uis.JumpRequest)) do 
        v:Enable()    
    end
end
for k,v in pairs(plr.PlayerGui.ScreenGui:GetChildren()) do 
    if v.Name=="TileGrid" then 
        table.insert(ListTileGrid,v)
    end
end
local SaveFileName = getgenv().SaveFileName or plr.Name.."_BeeSwarmSimulator.json"

function SaveSettings()
    local HttpService = game:GetService("HttpService")
    if not isfolder("Sea Hub") then
        makefolder("Sea Hub")
    end
    writefile("Sea Hub/" .. SaveFileName, HttpService:JSONEncode(Settings))
end

function ReadSetting() 
    local s,e = pcall(function() 
        local HttpService = game:GetService("HttpService")
        if not isfolder("Sea Hub") then
            makefolder("Sea Hub")
        end
        return HttpService:JSONDecode(readfile("Sea Hub/" .. SaveFileName))
    end)
    if s then return e 
    else
        SaveSettings()
        return ReadSetting()
    end
end
Settings = ReadSetting()

if getgenv().WebHookLink then 
    Settings.WebHookUrl = getgenv().WebHookLink
end
if getgenv().DisableConvert then Settings.DisableConvert = true end
if getgenv().CustomSetting then 
    for k,v in pairs(getgenv().CustomSetting) do 
        Settings[k] = v
    end
end

function GetPlrHive() 
    for _, v in pairs(game.Workspace.Honeycombs:GetChildren()) do
        if tostring(v.Owner.Value) == plr.Name then
            return v
        end
    end
end

wait(1)
for k,v in pairs(game:GetService("Workspace").Gates:GetChildren()) do 
	for k,v in pairs(v:GetChildren()) do 
		pcall(function() 
			v.CanCollide=false
		end)
	end
end
local LevelFarm = {"CurrentField","QuestPollen","QuestField","FieldBoost","QuestMob","Guiding","Sprout","Pushroom","StickBug","Metor","Mob"}
local ListAllToken = {}
local ListAllDupedToken = {}
local StopFarm = {"Farm","SetHeight", "FTPrio", "Snail","Metor","Kill","Stocking","Snowflake","Rare","Leaf","Firefly","Donate","Planter","Stick","Ant","Dispenser","Craft","Memory","FieldBoost","tuoidz","StopMoreOne"}

local listjelly = {"Crimson","Cobalt","Festive","Gummy","Photon","Puppy","Tabby","Vicious","Windy"}
for k,v in pairs(listjelly) do 
    listjelly[k]=listjelly[k].."BeeJelly"    
end
table.insert(listjelly,"RoyalJelly")
function Tele(cf) 
    if plr.Character:FindFirstChild("HumanoidRootPart") then 
        plr.Character.HumanoidRootPart.CFrame=cf
    end
end

function GetHumanoidRootPart() 
    if plr.Character then 
        return plr.Character:FindFirstChild("HumanoidRootPart")
    end
end

function GetHop() 
    local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
    AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
    table.insert(AllIDs, actualHour)
    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
    local Site;
    if foundAnything == "" then
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
    else
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
    end
    local ID = ""
    if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
        foundAnything = Site.nextPageCursor
    end
    local num = 0;
    for i,v in pairs(Site.data) do
        local Possible = true
        ID = tostring(v.id)
        if tonumber(v.maxPlayers) > tonumber(v.playing) then
            for _,Existing in pairs(AllIDs) do
                if num ~= 0 then
                    if ID == tostring(Existing) then
                        Possible = false
                    end
                else
                    if tonumber(actualHour) ~= tonumber(Existing) then
                        local delFile = pcall(function()
                            delfile("NotSameServers.json")
                            AllIDs = {}
                            table.insert(AllIDs, actualHour)
                        end)
                    end
                end
                num = num + 1
            end
            if Possible == true then
                table.insert(AllIDs, ID)
                wait()
                pcall(function()
                    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                    wait()
                    game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, plr)
                end)
                wait(4)
            end
        end
    end
end
function GetMemoListName()
    local tab = {}
    for k, v in pairs(game.Workspace.Toys:GetChildren()) do
        if string.match(v.Name, "Memory Match") then
            table.insert(tab, v.Name)
        end
    end
    return tab
end
 function Teleport()
    while wait() do
        pcall(function()
            TPReturner()
            if foundAnything ~= "" then
                TPReturner()
            end
        end)
    end
end
return Teleport
end
Hop = GetHop()

local SpawnTable = {}

pcall(function() 
    game:GetService("Workspace").Decorations["30BeeZone"].Pit.TouchInterest:Destroy()
end)
for k,v in pairs(game:GetService("Workspace")["Invisible Walls"]:GetChildren()) do v:Destroy() end
for k,v in pairs(game:GetService("Workspace").Territories:GetChildren()) do v:Destroy() end
for k,v in pairs(game:GetService("Workspace").MonsterBarriers:GetChildren()) do v:Destroy() end

for k,v in pairs(game:GetService("Workspace").Map.OuterInvisWalls:GetChildren()) do v:Destroy() end
local TvkStatCache = game:GetService("ReplicatedStorage").Events.RetrievePlayerStats:InvokeServer()
spawn(function() 
    while wait(1) do 
        TvkStatCache =game:GetService("ReplicatedStorage").Events.RetrievePlayerStats:InvokeServer()
        getfenv().TvkStatCache = TvkStatCache
    end
end)
getfenv().TvkStatCache = TvkStatCache

Exploit = "Synapse X"
if http_request and secure_load then
    Exploit = "Sentinel"
    if syn then
        setreadonly(syn, false)
        syn.request = http_request
    else
        syn = {}
        syn.request = http_request
    end
end
function fspawn(f) 
    return coroutine.wrap(f)()
end
function mysplit(inputstr, sep)
    if sep == nil then
        sep = "%s"
    end
    local t = {}
    for str in string.gmatch(inputstr, "([^" .. sep .. "]+)") do
        table.insert(t, str)
    end
    return t
end
local FieldXYJSON = [[{"Mountain Top Field":{"Y":27,"X":23},"Bamboo Field":{"Y":17,"X":38},"Dandelion Field":{"Y":17,"X":35},"Pumpkin Patch":{"Y":16,"X":32},"Sunflower Field":{"Y":32,"X":19},"Mushroom Field":{"Y":22,"X":31},"Blue Flower Field":{"Y":16,"X":42},"Pine Tree Forest":{"Y":30,"X":22},"Strawberry Field":{"Y":25,"X":21},"Coconut Field":{"Y":20,"X":29},"Stump Field":{"Y":0,"X":0},"Spider Field":{"Y":25,"X":27},"Rose Field":{"Y":19,"X":30},"Ant Field":{"Y":12,"X":31},"Clover Field":{"Y":28,"X":25},"Pineapple Patch":{"Y":22,"X":32},"Cactus Field":{"Y":17,"X":32},"Pepper Patch":{"Y":26,"X":20}}]]
local FieldXY = game:GetService("HttpService"):JSONDecode(FieldXYJSON)

local FieldPart = {}
for k,v in pairs(game.Workspace.Flowers:GetChildren()) do 
    for k,v2 in pairs(game.Workspace.FlowerZones:GetChildren()) do 
        if v2:FindFirstChild("ID") then 
            local id = v2.ID.Value
            if mysplit(v.Name,"-")[1] == "FP"..id then 
                if not FieldPart[v2.Name] then 
                    FieldPart[v2.Name] = {}
                end
                table.insert(FieldPart[v2.Name],v)
            end
        end
    end    
end

function CountMark(Field,a,b,c) 
    -- local OverlapParams = Instance.new("OverlapParams")
    -- OverlapParams.FilterDescendantsInstances = {}
    local count = 0
    for k, v in ipairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part")
        and v.Name == "AreaRing"
        and getgenv().IsValidTokenPos(v, Field) then
            if IsInTriagule(v.Position,a,b,c) then 
                count = count+1
            end
        end
    end
    return count 
end


function triangle_area(x1, y1, x2, y2, x3, y3)
    return math.abs((x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)) / 2)
  end
  function barycentric_coordinates(x, y, ax, ay, bx, by, cx, cy)
    local u = ((by - cy) * (x - cx) + (cx - bx) * (y - cy)) / ((by - cy) * (ax - cx) + (cx - bx) * (ay - cy))
    local v = ((cy - ay) * (x - cx) + (ax - cx) * (y - cy)) / ((bx - cx) * (ay - cy) - (ax - cx) * (by - cy))
    local w = 1 - u - v
    return u, v, w
  end
  
  function is_point_in_triangle(x, y, ax, ay, bx, by, cx, cy)
    local u, v, w = barycentric_coordinates(x, y, ax, ay, bx, by, cx, cy)
    return u >= 0 and v >= 0 and w >= 0
  end
  -- Function to build a k-d tree
  local function build_kd_tree(points, depth)
    local axis = depth % 2
    if #points <= 1 then
      return points[1]
    end
    local xory
    if axis == 0 then xory = "x" else xory="y" end
    table.sort(points, function(a, b)
      return a[xory] < b[xory]
    end)
    local median = #points / 2
    local left_points = {}
    for i = 1, median do
      left_points[i] = points[i]
    end
    local right_points = {}
    for i = median + 1, #points do
      right_points[i - median] = points[i]
    end
    local node = {}
    node.point = points[median]
    node.left = build_kd_tree(left_points, depth + 1)
    node.right = build_kd_tree(right_points, depth + 1)
    return node
  end
  
  -- Function to search for the point C with maximum number of points inside the triangle ABC
  function search_point_c(node, a, b, c)
    if node == nil then return 0 end
    --print(node.point)
    if not node.point then return 0 end
    local count = 0
    if is_point_in_triangle(node.point.x, node.point.y,a.x, a.y, b.x, b.y, c.x, c.y) then
      count = count + 1
    end
    local left_count = search_point_c(node.left, a, b, c)
    local right_count = search_point_c(node.right, a, b, c)
    
    return count + left_count + right_count
  end
  
  -- Function to find the point C with maximum number of points inside the triangle ABC
  function find_point_c(kd_tree, points, a, b)
    local max_points, max_point = 0, nil
    for _, c in ipairs(points) do
      local count = search_point_c(kd_tree, a, b, c)
      if count > max_points then
        max_points = count
        max_point = c
      end
    end
    return max_point, max_points
  end
function GetBestTriagulatePoint(Field,a,b) 
    local points = {}
    if FieldPart[Field] then 
        for k,v in pairs(FieldPart[Field]) do 
            table.insert(points,{x=v.Position.X,y=v.Position.Z})
        end
    end
    local listmark = {}
    for k, v in ipairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part")
        and v.Name == "AreaRing"
        and getgenv().IsValidTokenPos(v, Field) then
            table.insert(listmark,{x=v.Position.X,y=v.Position.Z})
        end
    end
    local tree = build_kd_tree(listmark,0)
    return find_point_c(tree,points,{x=a.X,y=a.Z},{x=b.X,y=b.Z})
end


local Con = {}
local Selling = false
function GetListField(a)
    local tablee = {}
    for _, v in pairs(game.Workspace.FlowerZones:GetChildren()) do
        table.insert(tablee, v.Name)
    end
    if a then 
        table.insert(tablee,a)
    end
    return tablee
end
function ListToOb(tabl, tf)
    local out = {}
    for k, v in pairs(tabl) do
        if tf then
            out[v] = true
        else
            out[v] = false
        end
    end
    return out
end

local StopFarmVK = vToK(StopFarm)
local StopFarmList = ToST(StopFarmVK,false)
local SupportedList = {
    "Polar Bear",
    "Brown Bear",
    "Black Bear",
    "Science Bear",
    "Bucko Bee",
    "Riley Bee",
    "Panda Bear",
    "Spirit Bear",
    "Onett"
}
local UnSupported = {
    'Mother Bear','Bubble Bee Man 2','Stick Bug','Gummy Bear',
}
local UnSupportedR = {}
for k,v in pairs(UnSupported) do 
    table.insert(UnSupportedR,v.." (Not fully supported)")
end

local QuestList = {}
for k,v in pairs(SupportedList) do 
    table.insert(QuestList,v)
end
-- for k,v in pairs(UnSupported) do 
--     table.insert(QuestList,v.." (Not fully supported)")
-- end
local BadgeRank = {
    "Cadet","Hotshot","Ace","Master","Grandmaster"
}

local BadgeRankTF = ListToOb(BadgeRank, false)
if not Settings.BadgeRankTF then Settings.BadgeRankTF = BadgeRankTF else  for k,v in pairs(Settings.BadgeRankTF) do 
    BadgeRankTF[k]=v 
end
Settings.BadgeRankTF=BadgeRankTF
end

local BadgeRankTF2 = ListToOb(BadgeRank, false)
if not Settings.BadgeRankTF2 then Settings.BadgeRankTF2 = BadgeRankTF2 else  for k,v in pairs(Settings.BadgeRankTF2) do 
    BadgeRankTF2[k]=v
end
Settings.BadgeRankTF2=BadgeRankTF2
end


local FieldListT = GetListField()
local FieldListTFBadge = ListToOb(FieldListT, false)

if not Settings.FieldListTFBadge then Settings.FieldListTFBadge = FieldListTFBadge else  for k,v in pairs(Settings.FieldListTFBadge) do 
    FieldListTFBadge[k]=v
end
Settings.FieldListTFBadge=FieldListTFBadge
end


local QuestTF = ListToOb(QuestList, true)

if not Settings.QuestTF then Settings.QuestTF = QuestTF else  for k,v in pairs(Settings.QuestTF) do 
    QuestTF[k]=v
end
Settings.QuestTF=QuestTF
end

local QuestTFFast = ListToOb({"Polar Bear","Riley Bee","Bucko Bee"}, false)

if not Settings.QuestTFFast then Settings.QuestTFFast = QuestTFFast else  for k,v in pairs(Settings.QuestTFFast) do 
    QuestTFFast[k]=v
end
Settings.QuestTFFast=QuestTFFast
end

local ColorL = {
    "Red","Blue","White"
}
local ColorLTF = ListToOb(ColorL, true)
if not Settings.ColorLTF then Settings.ColorLTF = ColorLTF else  for k,v in pairs(Settings.ColorLTF) do 
    ColorLTF[k]=v
end
Settings.ColorLTF=ColorLTF
end


local PuffRaity = {
    "Mythic","Legendary","Epic","Rare","Normal"
}
local PuffRaityTF = ListToOb(PuffRaity, true)

if not Settings.PuffRaityTF then Settings.PuffRaityTF = PuffRaityTF else  for k,v in pairs(Settings.PuffRaityTF) do 
    PuffRaityTF[k]=v
end
Settings.PuffRaityTF=PuffRaityTF
end


local TPuffRaityTF = ListToOb(PuffRaity, false)
if not Settings.TPuffRaityTF then Settings.TPuffRaityTF = TPuffRaityTF else  for k,v in pairs(Settings.TPuffRaityTF) do 
    TPuffRaityTF[k]=v
end
Settings.TPuffRaityTF=TPuffRaityTF
end

local PFieldTF = ListToOb(GetListField(), true)
if not Settings.PFieldTF then Settings.PFieldTF = PFieldTF else  for k,v in pairs(Settings.PFieldTF) do 
    PFieldTF[k]=v
end
Settings.PFieldTF=PFieldTF
end



local MemoList = GetMemoListName()
local MemoTF = ListToOb(MemoList,false)

if not Settings.MemoTF then 
    Settings.MemoTF=MemoTF
else
    MemoTF=Settings.MemoTF
end


local AntMethod = ""



function CheckFarm(name) 
    local index = StopFarmVK[name]
    if index then 
        for i=index+1,#StopFarm do 
            if StopFarmList[StopFarm[i]] then 
                return false
            end
        end
        return true
    end
    return false
end

local TokenId = {
    ["Ticket"] = "rbxassetid://1674871631",
    ["Glue"] = "rbxassetid://2504978518",
    ["Pineapple"] = "rbxassetid://1952796032",
    ["Strawberry"] = "1952740625",
    ["Blueberry"] = "rbxassetid://2028453802",
    ["SunflowerSeed"] = "rbxassetid://1952682401",
    ["Treat"] = "rbxassetid://2028574353",
    ["Gumdrop"] = "rbxassetid://1838129169",
    ["Red Extract"] = "2495935291",
    ["Blue Extract"] = "rbxassetid://2495936060",
    ["Oil"] = "2545746569",
    ["Glitter"] = "rbxassetid://2542899798",
    ["Enzymes"] = "rbxassetid://2584584968",
    ["TropicalDrink"] = "3835877932",
    ["Diamond Egg"] = "rbxassetid://1471850677",
    ["Gold Egg"] = "rbxassetid://1471849394",
    ["Mythic Egg"] = "4520739302",
    ["Star Treat"] = "rbxassetid://2028603146",
    ["Royal Jelly"] = "rbxassetid://1471882621",
    ["Star Jelly"] = "rbxassetid://2319943273",
    ["Moon Charm"] = "rbxassetid://2306224708",
    ["Super Smoothie"] = "5144657109",
    ["Bitterberry"] = "4483236276",
    ["Festive Bean"] = "4483230719",
    ["Ginger Bread"] = "6077173317",
    ["Aged Ginger Bread"] = "6077173317",
    ["Honey Token"] = "1472135114",
    ["Purple Poition"] = "4935580111",
    ["Snowflake"] = "6087969886",
    ["Magic Bean"] = "2529092020",
    ["Neonberry"] = "4483267595",
    ["Swirled Wax"] = "8277783113",
    ["Soft Wax"] = "8277778300",
    ["Hard Wax"] = "8277780065",
    ["Caustic Wax"] = "827778166",
}
local TokenId2 = {
    ["Bitterberry2"] = "4483230719"
}

local PrioritizeList = {
    ["Token Link"] = "1629547638",
    ["Inspire"] = "2000457501",
    ["Bear Morph"] = "177997841",
    ["Polen Bomb"] = "1442725244",
    ["Fuzz Bomb"] = "4889322534",
    ["Polen Haze"] = "4889470194",
    ["Triangulate"] = "4519523935",
    ["Inferno"] = "4519549299",
    ["Summon Frog"] = "4528414666",
    ["Tornado"] = "3582519526",
    ["Cross Hair"] = "rbxassetid://8173559749",
    ["Red Boost"] = "1442859163",
    ["Inflate Ballon"] = "8083437090"
}
local ItemDonateList = {
    "Ticket",
    "Gumdrops",
    "Coconut",
    "Stinger",
    "Micro-Converter",
    "FieldDice",
    "JellyBeans",
    "RedExtract",
    "BlueExtract",
    "Glitter",
    "Glue",
    "Oil",
    "Enzymes",
    "TropicalDrink",
    "MagicBean",
    "CloudVial",
    "Box-O-Frogs",
    "AntPass",
    "Treat",
    "SunflowerSeed",
    "Strawberry",
    "Pineapple",
    "Blueberry",
    "Bitterberry",
    "Neonberry",
    "Moon Charm",
    "BasicEgg",
    "SilverEgg",
    "DiamondEgg",
    "RoyalJelly",
    "Gold",
    "PurplePotion"
}
for k, v in pairs(TokenId) do
    PrioritizeList[k] = v
end
function CheckToyCD(toy) 
    local cd = game.Workspace.Toys[toy].Cooldown.Value
        if not TvkStatCache.ToyTimes[toy] then return true end
        return os.time()-TvkStatCache.ToyTimes[toy] > cd
end

local PrioritizeListTF = ToTrueFalse(PrioritizeList)
PrioritizeListTF["Token Link"] = true
if not Settings.PrioritizeListTF then
    Settings.PrioritizeListTF = PrioritizeListTF
else
    for k,v in pairs(Settings.PrioritizeListTF) do 
        PrioritizeListTF[k]=v
    end
    Settings.PrioritizeListTF = PrioritizeListTF
end

local IgnoreListTF = ToTrueFalse(PrioritizeList)
if not Settings.IgnoreListTF then
    Settings.IgnoreListTF = IgnoreListTF
else
    for k,v in pairs(Settings.IgnoreListTF) do 
        IgnoreListTF[k]=v
    end
    Settings.IgnoreListTF = IgnoreListTF
end

function SetupTF(TF,Name) 
    local ListTF = ListToOb(TF)
    
    if not Settings[Name] then Settings[Name] = ListTF else  for k,v in pairs(Settings[Name]) do 
        ListTF[k]=v
    end Settings[Name] = ListTF end
    return ListTF
end
function SetupTFNor(ListTF,Name)     
    if not Settings[Name] then Settings[Name] = ListTF else  for k,v in pairs(Settings[Name]) do 
        ListTF[k]=v
    end Settings[Name] = ListTF end
    return ListTF
end
local NoSell = false

local AutoGum = false
local AutoCoco = false
local TypeFarming = "Walk"
local AutoDig = false

local StopMoreOne = false
local Valid = true
local InsValid = 26110

local AutoRare = false
local TokenIdByK = vToK(TokenId)
local TokenTrueFakse = ToTrueFalse(TokenId)
local TokenTrueFakse2 = ToTrueFalse(TokenId)
local PlantMagic = false
local HoneyPolen = {
    ["Honey"] = true,
    ["Pollen"] = true
}
local BarId = {
    ["Glue"] = "rbxassetid://2504978518",
    ["Oil"] = "rbxassetid://2545746569",
    ["Enzymes"] = "rbxassetid://2584584968",
    ["Tropical Drink"] = "3835877932",
    ["Blue Extract"] = "rbxassetid://2495936060",
    ["Red Extract"] = "rbxassetid://2495935291",
    ["Stinger"] = "2314214749",
    ["Gumdrop"] = "rbxassetid://1838129169"
}
local FieldIconID = {
    ["Sunflower Field"] = "rbxassetid://2908769405",
    ["Dandelion Field"] = "rbxassetid://2908769047",
    ["Strawberry Field"] = "rbxassetid://2908769330",
    ["Blue Flower Field"] = "rbxassetid://2908768899",
    ["Clover Field"] = "rbxassetid://2908768973",
    ["Mushroom Field"] = "rbxassetid://2908769124",
    ["Spider Field"] = "rbxassetid://2908769301",
    ["Bamboo Field"] = "rbxassetid://2908768829",
    ["Pineapple Patch"] = "rbxassetid://2908769153",
    ["Stump Field"] = "rbxassetid://2908769372",
    ["Cactus Field"] = "rbxassetid://2908768937",
    ["Pumpkin Patch"] = "rbxassetid://2908769220",
    ["Pine Tree Forest"] = "rbxassetid://2908769190",
    ["Rose Field"] = "rbxassetid://2908818982",
    ["Coconut Field"] = "rbxassetid://2908769010",
    ["Mountain Top Field"] = "rbxassetid://2908769086",
    ["Ant Field"] = "rbxassetid://2908768728",
    ["Pepper Patch"] = "3835712489"
}
local Sprinklers = {
    ["The Supreme Saturator"] = 1,
    ["Basic Sprinkler"] = 1,
    ["Silver Soakers"] = 2,
    ["Golden Gushers"] = 3,
    ["Diamond Drenchers"] = 4
}
local TimerMob = {
    ["Rhino Beetle"] = {"Rhino Bush", "Rhino Cave 1", "Rhino Cave 2", "Rhino Cave 3", "PineappleBeetle"},
    ["Spider"] = {"Spider Cave"},
    ["Werewolf"] = {"WerewolfCave"},
    ["Scorpion"] = {"RoseBush", "RoseBush2"},
    ["Mantis"] = {"ForestMantis1", "ForestMantis2", "PineappleMantis1"},
    ["Ladybug"] = {"MushroomBush", "Ladybug Bush", "Ladybug Bush 2", "Ladybug Bush 3"}
}
local TimerKiet = ToTrueFalse(TimerMob, true)

if not Settings.TimerKiet then 
    Settings.TimerKiet=TimerKiet
else
    TimerKiet=Settings.TimerKiet
end
local fieldlistpolar = {
    "Spider Field",
    "Mushroom Field",
    "Rose Field",
    "Strawberry Field",
    "Bamboo Field",
    "Pumpkin Patch",
    "Sunflower Field",
    "Cactus Field",
    "Blue Flower Field",
    "Clover Field",
    "Pineapple Patch",
    "Dandelion Field",
    "Pine Tree Forest"
}
local moblistpolar = {
    "Spider",
    "Scorpion",
    "Werewol",
    "Mantises",
    "Ladybug",
    "Rhino Beetles"
}
local MaskField = {
    ["White"] = {
        "Sunflower Field",
        "Dandelion Field",
        "Spider Field",
        "Pineapple Patch",
        "Pumpkin Patch",
        "Coconut Field"
    },
    ["Blue"] = {
        "Blue Flower Field",
        "Bamboo Field",
        "Pine Tree Forest",
        "Stump Field"
    },
    ["Red"] = {
        "Mushroom Field",
        "Clover Field",
        "Strawberry Field",
        "Cactus Field",
        "Rose Field",
        "Pepper Patch",
        "Mountain Top Field",
        "Ant Field"
    }
}
local ShopList = {
}
for _,v in pairs(game.Workspace.Shops:GetChildren()) do 
    table.insert(ShopList,v.Name)
end
for _, v in pairs(game.Workspace.Collectibles:GetChildren()) do
    local Black = Instance.new("IntValue")
    Black.Parent = v
    Black.Name = "Blacklisted"
end
local AutoSprout = false
local times = 0.2
local Running = true
local Invisible = false
local Particles = game.Workspace.Particles
local Folder2 = Particles.Folder2
local vu = game:GetService("VirtualUser")
local x = 0
local y = 0
local QuestF = plr.PlayerGui.ScreenGui.Menus.Children.Quests.Content
local MaskF = {
    ["White"] = "Gummy Mask",
    ["Red"] = "Demon Mask",
    ["Blue"] = "Diamond Mask"
}
MaskF = SetupTFNor(MaskF,"MaskF")
plr.Idled:connect(
    function()
        vu:Button2Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
        wait(1)
        vu:Button2Up(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
    end
)
for i, v in pairs(workspace.FieldDecos:GetChildren()) do
    v:Destroy()
end
function GetFieldByName(name)
    return game.Workspace.FlowerZones:FindFirstChild(name)
end
function GetFieldId(name)
    return GetFieldByName(name).ID.Value
end


local maxx = 31
local maxy = 12

function GetFlower(field, x, y)
    local part = game.Workspace.Flowers:FindFirstChild(tostring(field) .. "-" .. tostring(x) .. "-" .. tostring(y))
    return part
end
function GetXY(part)
    local name = mysplit(part.name, "-")
    return unpack(name)
end
function Conv2LayerTable(tab)
    local tabl = {}
    for k, v in pairs(tab) do
        for f, s in pairs(v) do
            tabl[s] = k
        end
    end
    return tabl
end
local MaskField2 = Conv2LayerTable(MaskField)
local ValidTB={}
function ValidFarm()
    return CheckFarm("Farm")
end
for _, v in pairs(game.Workspace.Decorations.Misc:GetChildren()) do
    if string.match(v.Name, "Mushroom") or string.match(v.Name, "Blue Flower") then
        if v:IsA("Model") and #v:GetChildren() ~= 6 then
            for _, v in pairs(v:GetChildren()) do
                if v:IsA("Part") then
                    v.Transparency = 0.5
                    v.CanCollide = false
                end
            end
        end
    end
end
function GetFieldByFP(name) 
    local dit = name
    for k,v in pairs(GetListField()) do 
        local id = GetFieldId(v)
        if dit=="FP"..id then 
            return v
        end
    end
end
getgenv().IsValidTokenPos = function(token, Field,infield,sucvatruabithieunangvathanhtuoicungbithieunangvandokhongbithieunangttdbithieunangbrosabithieunangtvkkhongbithieunang)
    local pos
    if type(token) == "vector" then 
        pos = token
    else
        pos = token.Position
    end

    local kc = 60
    local Field = GetFieldByName(Field)
    if Field:FindFirstChild("Range") then kc=Field.Range.Value end
    local bool = false
    local Character = plr.Character
    local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
    
    if not infield and Field.Name~="PuffField" then 
        local ray = Ray.new(pos+Vector3.new(0,5,0), Vector3.new(0, -1000, 0))

        local thieutvknang = workspace:FindPartOnRayWithWhitelist(ray, {game.Workspace.Flowers})
        if thieutvknang then 
            local curr,x,y = GetXY(thieutvknang)
            local CurrentField = GetFieldByFP(curr)
            if CurrentField == Field.Name then 
               return math.abs(pos.Y-thieutvknang.Position.Y) 
            end
        end
    else
        
        if (pos - Field.Position).magnitude < kc then
            if infield then 
                for k,v in pairs(infield.List) do
                    if (pos-v.p).magnitude>infield.Range then return false end
                end
            end
            return math.abs(pos.Y-Field.Position.Y) 
        end
    end
end
function IsValidCharactPos(Field)
    local bool = false
    local Character = plr.Character
    
    local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
    if not IsValidTokenPos(Character.HumanoidRootPart,Field) then return false end
    local Field = GetFieldByName(Field)
    local kc = 100
    if Field:FindFirstChild("Range") then kc=Field.Range.Value end
    if (Field.Position - HumanoidRootPart.Position).magnitude < kc then
        bool = true
    end
    
    
    return bool
end

    getgenv().IsTokenBlacklist = function(token)
    if token:FindFirstChild("Blacklisted") then
        return true
    end
    return false
end

getgenv().IsToken = function(token)
    if token == nil then
        return false
    end
    if not token.Parent then return false end
    if token then
        if token.Orientation.Z ~= 0 then
            return false
        end
        if token:FindFirstChild("FrontDecal") then
        else
            return false
        end
        if not token.Name == "C" then
            return false
        end
        if not token:IsA("Part") then
            return false
        end
        return true
    else
        return false
    end
end
function CountSprink(name,pos) 
    local cc = 0
    for k,v in ipairs(game:GetService("Workspace").Gadgets:GetChildren()) do 
        if v.Name==name and v:FindFirstChild("Base") then 
            if (v.Base.Position-pos).magnitude<30 then 
                cc=cc+1
            end
        end
    end
    return cc
end
function CountTab(tab)
    local c = 0
    for k, v in pairs(tab) do
        c = c + 1
    end
    return c
end
function GetCurrentFieldBoost()
    local tab = {}
    for k,v in pairs(ListTileGrid) do 
        local GUI = v
        for _, v in pairs(GUI:GetChildren()) do
            if v.Name == "IconTile" and v:FindFirstChild("BG") then
                for f, s in pairs(FieldIconID) do
                    if
                        v.BG:FindFirstChild("Icon") and v.BG:FindFirstChild("Text") and v.BG:FindFirstChild("Bar") and
                            v.BG.Icon.Image == s and
                            v.BG.Bar.BackgroundColor3 == Color3.fromRGB(255, 228, 81)
                     then
                        tab[f] = v.BG.Text.Text
                    end
                end
            end
        end
    end
    
    return tab
end
function IsAnyBoost()
    local t = GetCurrentFieldBoost()
    for k, v in pairs(t) do
        return true
    end
    return false
end
function IsBoostEnd(Field)
    for k,v in pairs(ListTileGrid) do 
        local GUI = v
    for _, v in pairs(GUI:GetChildren()) do
        if v.Name == "IconTile" and v:FindFirstChild("BG") then
            for f, s in pairs(FieldIconID) do
                if
                    v.BG:FindFirstChild("Icon") and v.BG:FindFirstChild("Text") and v.BG:FindFirstChild("Bar") and
                        v.BG.Icon.Image == s and
                        v.BG.Bar.BackgroundColor3 == Color3.fromRGB(255, 228, 81)
                 then
                    if f == Field then
                        return false
                    end
                end
            end
        end
    end
    end
    
    return true
end

-- Get Mob Function

local AttackTokens = {
    "rbxassetid://1629547638",
    "rbxassetid://2319083910",
    "rbxassetid://1442700745",
    "rbxassetid://1629649299"
}
function CollectAttackTokens(x,all,IgnoreY)
    local sucvat =  plr.Character:WaitForChild("HumanoidRootPart").CFrame

    x = x or 50
    for k, v in pairs(game.workspace.Collectibles:GetChildren()) do
        local pass = true
        if not all then 
            if v:FindFirstChild("FrontDecal") then 
                pass = table.find(AttackTokens, v.FrontDecal.Texture) 
            end
        end
        if v.Name == "C"
        and not v:FindFirstChild("Ignored")
        and v:FindFirstChild("FrontDecal")
        and pass
        and (v.Position - plr.Character:WaitForChild("HumanoidRootPart").CFrame.Position).magnitude <= x then
            local cac
            if IgnoreY then 
                if (v.Position.Y - sucvat.Position.Y +3) > 0 then 
                    cac=true 
                end
            end
            if not cac then 
                plr.Character:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(v.Position) + Vector3.new(0, 3, 0)
                wait(.2)
                local ractvk = Instance.new("IntValue", v)
                ractvk.Name = "Ignored"
            end
           
        end
    end
end

function CollectTokenThanhTuoi(Field,TokenList)
    local collected = false
    for k, v in pairs(game.workspace.Collectibles:GetChildren()) do
        local pass = false
        if v:FindFirstChild("FrontDecal") then 
            for k,v2 in pairs(TokenList) do 
                if string.match(v.FrontDecal.Texture,v2) then pass = true break end
            end
            --pass = table.find(TokenList, v.FrontDecal.Texture) 
        end
        if v.Name == "C"
        and not v:FindFirstChild("Ignored")
        and v:FindFirstChild("FrontDecal")
        and pass then
            if IsToken(v) and IsValidTokenPos(v,Field) and not v:FindFirstChild("Ignored") then 
                local cac
                if not cac then 
                    StopFarmList["Firefly"] = true
                    Walkk(v.CFrame)
                    local ractvk = Instance.new("IntValue", v)
                    ractvk.Name = "Ignored"
                    game.Debris:AddItem(ractvk,2)
                end
            end
        end
    end
    return collected
end

function GetTunnel()
    for _, v in ipairs(game.Workspace.Monsters:GetChildren()) do
        if string.match(v.Name, "Tunnel") then
            if v:FindFirstChild("Config") then
                if v:FindFirstChild("Hunter") then
                    if v.Hunter.Value == plr.UserId then
                        return v
                    end
                end
            end
        end
    end
end

function GetKing()
    for _, v in ipairs(game.Workspace.Monsters:GetChildren()) do
        if v.Name=="King Beetle (Lvl 7)" then
            if v:FindFirstChild("Config") then
                if v:FindFirstChild("Hunter") then
                    if v.Hunter.Value == plr.UserId then
                        return v
                    end
                end
            end
        end
    end
end

local ccsnail = false



function GetMobIns(Mob)
    return game.Workspace.MonsterSpawners:FindFirstChild(Mob)
end
function GetAttach(Mob)
    local Att = Mob:FindFirstChild("Attachment")
    if Att then
        return Att
    else
        return Mob:FindFirstChild("TimerAttachment")
    end
end

local MonsterTypeMD = require(game.ReplicatedStorage.MonsterTypes)

function CheckMob(Mob)
    if TimerMob[Mob]==nil then return end
    for k, v in pairs(TimerMob[Mob]) do
        local t = GetMobIns(v)
        if t then 
            local data = TvkStatCache.MonsterTimes
            local rac2 = data[v]
            if rac2 then 
                local Reduce = 0
                pcall(function() 
                    Reduce = TvkStatCache.ModifierCaches.Value.MonsterCooldownReduction._
                end)
                Reduce=1-Reduce
                local cac = os.time()-rac2
                local rac = MonsterTypeMD.Get(t.MonsterType.Value).Stats.RespawnCooldown
                if cac>rac*Reduce+(Settings.MobDelay or 30) then 
                    return {
                        Part = t,
                        Status = function()
                            local data = TvkStatCache.MonsterTimes
                            local rac2 = data[v]
                            local cac = os.time()-rac2
                            local rac = MonsterTypeMD.Get(t.MonsterType.Value).Stats.RespawnCooldown
                            return cac>rac*Reduce+(Settings.MobDelay or 30)
                        end
                    }
                end
            end
        end
    end
end
local a = require(game.ReplicatedStorage.Activatables.Toys)

local check1 = debug.getupvalue(a.ButtonEffect,1)
local check2 = debug.getupvalue(a.ButtonEffect,2)
function CheckToy(toy) 
    return warpF2(function() 
        return check1(a,toy) and check2(a,toy)   
    end)
end
function CheckCoco()
    local k = "CoconutCrab"
    local t = GetMobIns(k)
    if t then 
        if GetAttach(t).TimerGui.TimerLabel.Visible == false then
            return t
        end
    end
    
end
function CheckSnail()
    local k = "StumpSnail"
    local t = GetMobIns(k)
    if t then 
    if GetAttach(t).TimerGui.TimerLabel.Visible == false then
        return t
    end
end
end
function CheckTunnel()
    local k = "TunnelBear"
    local t = GetMobIns(k)
    if t then 
        if GetAttach(t).TimerGui.TimerLabel.Visible == false then
            return t
        end
    end
    
end
function reverse(t)
    local n = #t
    local i = 1
    while i < n do
      t[i],t[n] = t[n],t[i]
      i = i + 1
      n = n - 1
    end
    return t
  end
function CheckKing()
    local k = "King Beetle Cave"
    local t = GetMobIns(k)
    if t then 
        if GetAttach(t).TimerGui.TimerLabel.Visible == false then
            return t
        end
    end
    
end
function CheckComando()
    local k = "Commando Chick"
    local t = GetMobIns(k)
    if t then 
        if GetAttach(t).TimerGui.TimerLabel.Visible == false then
            return t
        end
    end
    
end

function GetCurrentAmountOfBee()
    local bee = 0
    for _, v in pairs(game.Workspace.Honeycombs:GetChildren()) do
        if tostring(v.Owner.Value) == plr.Name then
            for l, s in pairs(v.Cells:GetChildren()) do
                if s.CellType.Value ~= "Empty" and tostring(s.CellType.Value) ~= "nil" then
                    bee = bee + 1
                end
            end
        end
    end
    return bee
end
local sanghuman = require(game:GetService("ReplicatedStorage").BeeTypes).GetTypes()
function tuoidz(func) 
    spawn(function() 
        local Voiddz = 0
        local act6temp = 0
        local jimmy2 = game:GetService("ReplicatedStorage").Events.RetrieveCachedPlayerStat:InvokeServer("MaxBeeEnergy")
        local sangzboi = game:GetService("ReplicatedStorage").Events.RetrievePlayerStat:InvokeServer({"Honeycomb"})
        for k,v in pairs(sangzboi) do 
            for k,v in pairs(v) do 
                if v.Type and sanghuman[v.Type] then 
                    local act5 = 20
                    local thanhtuoi = sanghuman[v.Type].Bonuses
                    if thanhtuoi and thanhtuoi.MaxEnergy then 
                        for k,v in pairs(thanhtuoi.MaxEnergy) do 
                            if k=="Add" then act5=act5+v end
                            if k=="Mul" then act5=act5*v end
                        end
                    end
                    act5=act5*(1+0.05*(v.Lvl-1))
                    if jimmy2 then 
                        act5 = act5*jimmy2
                    end
                    if v.Mutas then 
                        if v.Mutas.Energy then 
                            act5 = act5*v.Mutas.Energy
                        end
                    end
                    if v.Energy==0 then v.Energy = act5 end
                    if v.Energy > 10^5 then v.Energy = act5 end
                    Voiddz=Voiddz+(v.Energy/act5)
                    act6temp = act6temp+1
                end
            end
        end
        func(Voiddz/act6temp)
    end)
end

function CountTabTF(tb) 
    local c = 0
    for k,v in pairs(tb) do 
    
    end
end
function SendHook()
    local HttpService = game:GetService("HttpService")
    local tb = {
        ["content"] = "",
        ["embeds"] = {{
            ["title"] = "Bee Swarm Simulator",
            ["description"] = "",
            ["type"] = "rich",
            ["color"] = tonumber(0xbdce44),
            ["fields"] = ListToField(),
            ["footer"] = {
                ["icon_url"] = "https://cdn.discordapp.com/attachments/832985237638086660/843786018892939284/turtle.png",
                ["text"] = "Sea Hub (" .. os.date("%X") .. ")"
            }
        }}
    }
    
    local a =
        syn.request(
        {
            Url = Settings.WebHookUrl,
            Method = "POST",
            Body = HttpService:JSONEncode(tb),
            Headers = {
                ["Content-Type"] = "application/json"
            }
        }
    )
    return a.Body
end
function SendHookCT(ct,content)
    local HttpService = game:GetService("HttpService")
    local tb = {
        ["content"] = content or "",
        ["embeds"] = {{
            ["title"] = "Bee Swarm Simulator",
            ["description"] = "",
            ["type"] = "rich",
            ["color"] = tonumber(0xbdce44),
            ["fields"] = ct,
            ["footer"] = {
                ["icon_url"] = "https://cdn.discordapp.com/attachments/832985237638086660/843786018892939284/turtle.png",
                ["text"] = "Sea Hub (" .. os.date("%X") .. ")"
            }
        }}
    }
    
    local a =
        syn.request(
        {
            Url = Settings.WebHookUrl,
            Method = "POST",
            Body = HttpService:JSONEncode(tb),
            Headers = {
                ["Content-Type"] = "application/json"
            }
        }
    )
    return a.Body
end
function SendHookContent(content)
    local HttpService = game:GetService("HttpService")
    local tb = {
        ["content"] = content or ""
    }
    
    local a =
        syn.request(
        {
            Url = Settings.WebHookUrl,
            Method = "POST",
            Body = HttpService:JSONEncode(tb),
            Headers = {
                ["Content-Type"] = "application/json"
            }
        }
    )
    return a.Body
end
local NPCLV = {
    [0] = {
        "Black Bear",
        "Mother Bear",
        "Brown Bear",
        "Riley Bee",
        "Bucko Bee",
        "Bee Bear 4"
    },
    [5] = {
        "Panda Bear"
    },
    [10] = {
        "Science Bear"
    },
    [15] = {
        "Polar Bear",
        "Honey Bee"
    },
    [30] = {
        "Onett"
    },
    [35] = {
        "Spirit Bear"
    }
}
local FieldLV = {
    [0] = {
        "Mushroom Field",
        "Blue Flower Field",
        "Sunflower Field",
        "Dandelion Field",
        "Clover Field",
        "PuffField"
    },
    [5]={
        "Strawberry Field",
        "Bamboo Field",
        "Spider Field"
    },
    [10] = {
        "Pineapple Patch",
        "Stump Field"
    },
    [15] = {
        "Rose Field",
        "Pine Tree Forest",
        "Pumpkin Patch",
        "Cactus Field"
    },
    [25] = {
        "Mountain Top Field"
    },
    [35] = {
        "Coconut Field",
        "Pepper Patch"
    }
}
function RedBlueWhite(bee)
    local FieldColor = {
        ["Red"] = "Strawberry Field",
        ["Blue"] = "Pine Tree Forest",
        ["White"] = "Pineapple Patch"
    }
    if bee < 5 then
        FieldColor["Red"] = "Mushroom Field"
        FieldColor["Blue"] = "Blue Flower Field"
        FieldColor["White"] = "Sunflower Field"
    else
        if bee >= 5 and bee < 15 then
            FieldColor["Red"] = "Strawberry Field"
            FieldColor["Blue"] = "Bamboo Field"
            FieldColor["White"] = "Spider Field"
        else
            if bee >= 15 then
                FieldColor["Red"] = "Rose Field"
                FieldColor["Blue"] = "Pine Tree Forest"
                FieldColor["White"] = "Pumpkin Patch"
                if bee >= 35 then
                    if not CheckCoco() then
                        FieldColor["White"] = "Coconut Field"
                    end
                    FieldColor["Red"] = "Pepper Patch"
                end
            end
        end
    end
    return FieldColor
end
local col = {"Red", "Blue", "White"}
local FieldColor = {
    ["Red"] = "Strawberry Field",
    ["Blue"] = "Pine Tree Forest",
    ["White"] = "Pineapple Patch"
}
function CheckQuestReq(Field) 
    local curr = GetCurrentAmountOfBee()
    for k,v in pairs(NPCLV) do 
        if table.find(v,Field) then 
            return curr>=k
        end
    end
   return false
end
function CheckFieldReq(Field) 
    local curr = GetCurrentAmountOfBee()
    for k,v in pairs(FieldLV) do 
        if table.find(v,Field) then 
            return curr>=k
        end
    end
   return false
end
--local secure_call = syn.secure_call



function newsclosure(f) 
    return function()
        local ret
        secure_call(function() 
            ret=f()
         end,game:GetService("Players").LocalPlayer.PlayerScripts.Listeners)
         return ret
    end
end

function GetQuestListMD()
    local v1 = require(game.ReplicatedStorage.Quests)

    local v5 = require(game.ReplicatedStorage.NPCs)
    local ListQuest = {}
    warpF2(function() 
        local v91 = TvkStatCache
        for v96, v97 in pairs(v91.Quests.Active) do
            local l__Name__98 = v97.Name
            local v99 = v1:Get(l__Name__98)
            
            if
                v99.NPC and v99.Theme ~= "Xmas" and not v99.Hidden and
                    (not v99.Expiration or require(game.ReplicatedStorage.OsTime)() < v99.Expiration)
             then
                local v101 = v1:Progress(l__Name__98, v91)
                local v102 = true
                local ListTask = {}
                for v103, v104 in ipairs(v99.Tasks) do
                    local v58 = v104.Description
                    if type(v58) ~= "string" then
                        v58 = v58(TvkStatCache)
                    end
                    local Task = {
                        Description = v58,
                        IsCompleted = function()
                            return warpF2(function() 
                                local v102 = true
                                local v91 = TvkStatCache
                                local v101 = v1:Progress(l__Name__98, v91)
                                if v101 and v101[v103] and v101[v103][1] < 1 then
                                    return false
                                end
                                return true
                            end)
                        end,
                        Type = v104.Type,
                        Zone = v104.Zone,
                        Item = v104.Item,
                        MonsterType = v104.MonsterType,
                        Tag = v104.Tag,
                        Color = v104.Color,
                        Toy = v104.Toy,
                        Name = v99.Name
                    }
                    table.insert(ListTask, Task)
                end
                ListQuest[v99.NPC] = ListTask
            end
        end
    end)
    return ListQuest
end

function GetQuestNPC(npc)
    local ListQuest = GetQuestListMD()
    for k, v in pairs(ListQuest) do
        if k == npc then
            return v
        end
    end
end
function GetQuestName(npc) 
    local ListQuest = GetQuestNPC(npc)
    if ListQuest then 
        for k,v in pairs(ListQuest) do 
            if v.Name then 
                return v.Name
            end
        end
    end
end
function GetQuestType(quest)
    local type = ""
    if quest.Type == "Collect Pollen" then
        if quest.Zone then
            type = "Zone"
        elseif quest.Color then
            type = "Color"
        else
            tpye = "Pollen"
        end
    elseif quest.Type == "Defeat Monsters" then
        type = "Kill"
    elseif quest.Type == "Use Items" then
        type = "Use"
    elseif quest.Type == "Use Toy" then
        type = "Toy"
    elseif quest.Type == "Collect Tokens" then
        type = "Token"
    elseif quest.Type == "Collect Goo" then
        if quest.Zone then
            type = "Zone"
        elseif quest.Tag then
            type = "Color"
        else
            type = "Goo"
        end
    end
    return type
end

function GetQuestTable(quest)
    local questtb = {}
    for k, v in pairs(quest) do
        local type = GetQuestType(v)
        if not questtb[type] then
            questtb[type] = {}
        end
        table.insert(questtb[type], v)
    end
    return questtb
end

function GetAntQuest(QuestTF)
    for k, v in pairs(QuestTF) do
        if v then
            local QuestNPC = GetQuestNPC(k)
            if QuestNPC then
                local QuestTb = GetQuestTable(QuestNPC)
                if QuestTb["Kill"] then
                    for k, v in pairs(QuestTb["Kill"]) do
                        if not v.IsCompleted() then
                            if v.MonsterType then
                                if string.match(v.MonsterType, "Ant") then
                                    return v
                                end
                            end
                        end
                    end
                end
            end
        end
    end
end



local PopStarAura = "5101328809"
function IsPopStar()
    for k,v in pairs(ListTileGrid) do 
        local PlGui = v
        for _,v in pairs(PlGui:GetChildren()) do 
            if v:FindFirstChild("BG") then 
                  if v.BG:FindFirstChild("Icon") then 
                        if string.match(v.BG.Icon.Image,PopStarAura) then return true end
                  end
            end
      
      end
    end
    
    return false
end
function IsScrochStarEquip()
    local cac = "5101327864"
    for k,v in pairs(ListTileGrid) do 
        local PlGui = v
        for _,v in pairs(PlGui:GetChildren()) do 
            if v:FindFirstChild("BG") then 
                  if v.BG:FindFirstChild("Icon") and not string.match(v.BG.Text.Text,"s") then 
                        if string.match(v.BG.Icon.Image,cac) then return true end
                  end
            end
        end
    end
    
    return false
end
function IsScrochStar() 
    local cac = "5101329167"
    for k,v in pairs(ListTileGrid) do 
        local PlGui = v
        for _,v in pairs(PlGui:GetChildren()) do 
            if v:FindFirstChild("BG") then 
                  if v.BG:FindFirstChild("Icon")  then 
                        if string.match(v.BG.Icon.Image,cac) then return true end
                  end
            end
        end
    end
    
    return false
end

function IsPrecise() 
    local cac = "rbxassetid://8172818074"
    for k,v in pairs(ListTileGrid) do 
        local PlGui = v
        for _,v in pairs(PlGui:GetChildren()) do 
            if v:FindFirstChild("BG") then 
                  if v.BG:FindFirstChild("Icon") then 
                        if string.match(v.BG.Icon.Image,cac) then return {Text = v.BG.Text.Text, Percent = v.BG.Bar.Size.Y.Scale} end
                  end
            end
        end
    end
    return false
end
function NearestCross(a) 
    local Gan
    local GanNhat
    for k,v in pairs(a) do 
        if #v == 3 then 
            local Nearest
            local c = 0

            local c2 = 0
            for k,v in pairs(v) do
                if not v.Part.Parent then 
                    c2=c2+1
                end 
                if not Nearest then Nearest = v end
                if v.Activated then c = c+1 end
                if (plr.Character.HumanoidRootPart.Position-v.Part.Position).magnitude < (plr.Character.HumanoidRootPart.Position-Nearest.Part.Position).magnitude then 
                    Nearest = v
                end
            end
            if c==3 then Nearest = nil end
            if c2== 3 then 
                Nearest = nil
            end
            if Nearest then 
                if not Gan then Gan = Nearest GanNhat = v end
                if (plr.Character.HumanoidRootPart.Position-Nearest.Part.Position).magnitude < (plr.Character.HumanoidRootPart.Position-Gan.Part.Position).magnitude then 
                    Gan = Nearest
                    GanNhat = v
                end
            end
        end
        
    end
    if GanNhat then return GanNhat end
end
local nll = require(game:GetService("ReplicatedStorage").BlenderRecipes)
local HttpService = game:GetService("HttpService")
function GetItemListWithValue()
    local StatCache = TvkStatCache
    local data = StatCache
    return data.Eggs
end
function CheckNguyenLieu(ng)
    local ind = nll.Get(ng)
    local k = false
    for k, v in pairs(ind.Ingredients) do
        local t = GetItemListWithValue()
        if t[v.Type] and (t[v.Type] >= v.Amount) then
        else
            k = true
            break
        end
    end
    if not k then
        return true
    else
        return false
    end
end


local cls = require(game.ReplicatedStorage.ClientStatCache)
local StatCache = require(game.ReplicatedStorage.ClientStatCache)
local ostime=require(game.ReplicatedStorage.OsTime)

local oldhoney = StatCache.Get().Totals.Honey
getgenv().HoneyMade = 0
spawn(function()
    while wait(4) do
        getgenv().HoneyMade = StatCache.Get().Totals.Honey - oldhoney
    end
end)

function GetCraftingStatus() 
local data = game:GetService("ReplicatedStorage").Events.RetrievePlayerStats:InvokeServer()
local blender = data.BlenderState

if not blender then return 0 end
local n = blender.Count
local Start = blender.StartTime

local v32 = data.PlaytimeAtLoad;
local v33 = data.LoadTime;
local v29 = blender

local v34 = v32 + (ostime() - v33) - v29.StartTime;
local f = (60*n*5-v34)/60
if f<=0 then return 1,blender end
return 2,blender
end
function FireTouch(part) 
    if plr.Character:FindFirstChild("HumanoidRootPart") then 
        firetouchinterest(plr.Character:WaitForChild("HumanoidRootPart"), part, 0)
        firetouchinterest(plr.Character:WaitForChild("HumanoidRootPart"), part, 1)    
    end
     
end
function God()
    Instance.new("BoolValue",plr.Character).Name="Godded"
    local cam = workspace.CurrentCamera
    local cf = cam.CFrame
    local me = plr
    local c, h =
        (me.Character or workspace:FindFirstChild(me.Name)),
        me.Character:FindFirstChildOfClass("Humanoid")
    local nh = h:Clone()
    nh.Health = nh.MaxHealth
    me.Character = nil
    nh:SetStateEnabled(15, false)
    nh:SetStateEnabled(1, false)
    nh:SetStateEnabled(0, false)
    nh.Parent = c
    h:Destroy()
    me.Character, cam.CameraSubject = c, nh
    wait()
    cam.CFrame = cf
    local s = c:FindFirstChild("Animate")
    if s then
        s.Disabled = true
        wait()
        s.Disabled = false
    end
    delay(
        1,
        function()
            if nh then
                nh.Health = 256
            end
        end
    )
    for i=1,10 do 
        FireTouch(game:GetService("Workspace").Map.Ground.Campsite.Lava)
    end
end
function GetItemListWithValue()
    local HttpService = game:GetService("HttpService")
    local StatCache = TvkStatCache
    local data = StatCache
    return data.Eggs
end
function GetItemList()
    local ks = GetItemListWithValue()
    local tb = {}
    for k, v in pairs(ks) do
        table.insert(tb, k)
    end
    return tb
end
function IsInstantValid(Instant)
    local replicatedstorage = game:GetService("ReplicatedStorage")
    local rep = replicatedstorage
    local r = require
    local player = plr

    local function getTimeSinceToyActivation(name)
        return r(rep.OsTime)() - r(rep.ClientStatCache):Get("ToyTimes")[name]
    end

    local function getTimeUntilToyAvailable(n)
        return workspace.Toys[n].Cooldown.Value - getTimeSinceToyActivation(n)
    end
    local StatCache = require(game.ReplicatedStorage.ClientStatCache)
    local gt = StatCache.Get()
    local toy = gt["ToyTimes"]
    if toy[Instant] then
        return getTimeUntilToyAvailable(Instant) <= 0
    else
        return false
    end
end

function UseInstant(Instant)
    game.ReplicatedStorage.Events.ToyEvent:FireServer(Instant)
end

function IsAnyInstantValid()
    local Lis = GetInstantList()
    for k, v in pairs(Lis) do
        if IsInstantValid(v.Name) then
            return true
        end
    end
    return false
end
function UnGod()
    if not plr.Character:FindFirstChild("Godded") then return end
    local cam = workspace.CurrentCamera
    local cf = cam.CFrame
    local me = plr
    local c, h =
        (me.Character or workspace:FindFirstChild(me.Name)),
        me.Character:FindFirstChildOfClass("Humanoid")
    local nh = h:Clone()
    nh.Health = nh.MaxHealth
    me.Character = nil
    nh:SetStateEnabled(15, true)
    nh:SetStateEnabled(1, true)
    nh:SetStateEnabled(0, true)
    nh.Parent = c
    h:Destroy()
    me.Character, cam.CameraSubject = c, nh
    wait()
    cam.CFrame = cf
    local s = c:FindFirstChild("Animate")
    if s then
        s.Disabled = false
        wait()
        s.Disabled = true
    end
    delay(
        1,
        function()
            if nh then
                nh.Health = 0
            end
        end
    )
end
function GetEquipSrinkler()
    local StatCache = require(game.ReplicatedStorage.ClientStatCache)
    return StatCache["Get"]()["EquippedSprinkler"]
end


loadstring([[
    function GetFieldByText(text) 
        for k,v in pairs(GetListField()) do 
            if string.match(text,v) then return v end
        end
    end
    function GetNerestFieldByObject(Obj)
        local lis = GetListField()
        local old = "Sunflower Field"
        for k, v in pairs(lis) do
            if v and v~="PuffField" then
                if
                    (Obj.Position - GetFieldByName(v).Position).magnitude <
                        (Obj.Position - GetFieldByName(old).Position).magnitude
                 then
                    old = v
                end
            end
        end
        return old
    end

]])()
function GetCurrentField() 
    if not plr.Character:FindFirstChild("HumanoidRootPart") then return end
    return GetNerestFieldByObject(plr.Character.HumanoidRootPart)
end


local ValidPos = {}

local Whitelist = {}

local ksf = nil




local HoneyTokenId="1472135114"




-- TVK LIB

    function GetTokenNearPos(pos,field,mag) 
        local FieldTokens = ListAllToken[field]
        if not FieldTokens then return end
        for k, ss in pairs(FieldTokens) do
            for k,v in ipairs(ss) do 
                if getgenv().IsToken(v) and getgenv().IsValidTokenPos(v, field,FieldPosIn,(Whitelist and #Whitelist>0)) and getgenv().isActiveTokens(v) and not getgenv().IsTokenBlacklist(v) then
                    local vthang = false 
                    if Whitelist and #Whitelist>0 then 
                        for k,v2 in pairs(Whitelist) do 
                            if string.find(v.FrontDecal.Texture,v2) then 
                                vthang = true
                            end
                        end
                    else
                        vthang = true
                    end
                    if vthang then 
                        if kc(v.Position) < mag then return v,true end
                    end
                end
            end
        end
    end
    function IsAnyPiro(Field,t,ListAllToken,FieldPosIn,Whitelist) 
        if not ListAllToken[Field] then return false end

        if Settings.GatherFlame then 
            local rac = GetListFire(Field)
            for k,v in pairs(rac) do 
                local nr = GetTokenNearPos(v.Position,Field,30)
                if nr then return true end
            end
        end
        for k,v in pairs(ListAllToken[Field]) do 
            if k~="None" then 
                for k,v  in pairs(v) do 
                    if getgenv().IsToken(v) and getgenv().IsValidTokenPos(v, Field,FieldPosIn,(Whitelist and #Whitelist>0)) and getgenv().isActiveTokens(v) and not getgenv().IsTokenBlacklist(v) then 
                        return true
                    end
                end
            end
        end
        return false
    end
    function GetNerestToken(Field,t,ListAllToken,FieldPosIn,Whitelist)
        local token
        local Character = plr.Character
        local HumanoidRootPart =t or Character:FindFirstChild("HumanoidRootPart")
        if not HumanoidRootPart then return end
        local h = HumanoidRootPart.Position
        local Piro = {}

        -- Mat cuoi dupe nha cmm
        if Settings.CollectDupe then 
            for k, v in pairs(game:GetService("Workspace").Camera.DupedTokens:GetChildren()) do
                if IsToken(v) and getgenv().IsValidTokenPos(v,Field) and not IsTokenBlacklist(v) then
                    if string.match(v.FrontDecal.Texture,"5877939956") then return v,true end
                end
            end
            for k, v in pairs(game:GetService("Workspace").Camera.DupedTokens:GetChildren()) do
                if IsToken(v) and getgenv().IsValidTokenPos(v,Field) and not IsTokenBlacklist(v) then
                    local BearMorphs = {"1472425802","1472580249","1472532912","1472491940"}
                    for k, v2 in pairs(BearMorphs) do 
                        if string.match(v.FrontDecal.Texture,v2) then return v,true end
                    end
                end
            end
            
        end
        
        local function SucVat(ListAllToken) 
            if not ListAllToken or not ListAllToken[Field] then return end

            local FieldTokens = ListAllToken[Field]
            for k, ss in pairs(FieldTokens) do
                if k~="None" then 
                    local tok
                    local ditme = k
                    for k,v in ipairs(ss) do 
                        if getgenv().IsToken(v) and getgenv().IsValidTokenPos(v, Field,FieldPosIn,(Whitelist and #Whitelist>0)) and getgenv().isActiveTokens(v) and not getgenv().IsTokenBlacklist(v) then
                            if ditme == "Token Link" then 
                                return v,true
                            end
                            local huhu = false 
                            if Whitelist and #Whitelist>0 then 
                                for k,v2 in pairs(Whitelist) do 
                                    if string.find(v.FrontDecal.Texture,v2) then 
                                        huhu = true
                                    end
                                end
                            else
                                huhu = true
                            end
                            if huhu then 
                                if (v.Position-h).magnitude < 3 then return v,true end
                                if not tok then tok=v end
                                if (v.Position-h).magnitude < (tok.Position-h).magnitude then 
                                    tok=v
                                end
                            end
                        end
                    end
                    if tok then 
                        Piro[tok]=(tok.Position-h).magnitude
                    end
                end
            end
            local sml
            for k,v in pairs(Piro) do 
                if not sml then sml=k end
                if v<Piro[sml] then sml=k end
            end
            if sml then return sml end
        end

        local tok

        local sucvat = SucVat(ListAllToken)
        if sucvat then return sucvat,true end

        if Settings.CollectDupe then 
            local ruabithieunang = SucVat(ListAllDupedToken)
            if ruabithieunang then return ruabithieunang,true end
        end
        if Settings.GatherFlame then 
            local rac = GetSortedFire(Field)
            for k,v in pairs(rac) do 
                local nr = GetTokenNearPos(v.Position,Field,30)
                if nr then  return nr,true end
            end
        end
        
        -- Piro token
        if ListAllToken[Field] then 
            --Normal token
            if ListAllToken[Field].None then 
                for _,v in ipairs(ListAllToken[Field].None) do 
                    if getgenv().IsToken(v) and getgenv().IsValidTokenPos(v, Field,FieldPosIn,(Whitelist and #Whitelist>0)) and getgenv().isActiveTokens(v) and not getgenv().IsTokenBlacklist(v) then 
                        local huhu = false 
                        if Whitelist and #Whitelist>0 then 
                            for k,v2 in pairs(Whitelist) do 
                                if string.find(v.FrontDecal.Texture,v2) then 
                                    huhu = true
                                end
                            end
                        else
                            huhu = true
                        end
                        if huhu then 
                            if not tok then tok=v end
                            if (v.Position-h).magnitude < (tok.Position-h).magnitude then 
                                tok=v
                            end
                        end 
                    end
                end
            end
            if tok then return tok end
        end
        if Settings.CollectDupe then 
            return GetNearestDupe(Field)
        end
    end


function NoFire(token) 
    local ray = Ray.new(token.Position+Vector3.new(0,1,0), Vector3.new(0, -5, 0))
    local t = workspace:FindPartOnRayWithIgnoreList(ray, {token,game.Workspace.Bees,plr.Character})
    if t and t:FindFirstChild("FireParticles") then 
        return false
    end

end
function CheckPollenValid(pollen) 
    local name,x,y=GetXY(pollen)
    if not name or not x or not y then return end
    x=tonumber(x)
    y=tonumber(y)
    local token = pollen
    
    if token then 
        if not NoFire(token) then return false end
    end

    local token = GetFlower(name,x,y+1)
    if token then 
        if not NoFire(token) then return false end
    end
    

    local token = GetFlower(name,x,y-1)

    if token then 
        if not NoFire(token) then return false end
    end

    local token = GetFlower(name,x+1,y)

    if token then 
        if not NoFire(token) then return false end
    end

    local token = GetFlower(name,x-1,y)

    if token then 
        if not NoFire(token) then return false end
    end
    return true
end
function GetComandoMob()
    for k, v in pairs(game.Workspace.Monsters:GetChildren()) do
        if string.match(v.Name, "Commando") then
            if v:FindFirstChild("Target")
            and v:FindFirstChild("Humanoid")
            and v:FindFirstChild("HumanoidRootPart") then
                if tostring(v.Target.Value) == plr.Name then
                    return v
                end
            end
        end
    end
end
local Temp = {
    Noclip = {}
}
function CheckEN(str)
    local cac = Temp[str]
    for k, v in pairs(cac) do
        if v then
            return true
        end
    end
    return false
end
function SetEN(str, cac, rac)
    Temp[str][cac] = rac
end
--setfflag("HumanoidParallelRemoveNoPhysics", "False")
--setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
game:GetService('RunService').Stepped:Connect(function()
    if CheckEN("Noclip") then plr.Character.Humanoid:ChangeState(11)
    end
end)
function kc(a,huhu)
    local nang = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
    if huhu then 
        a = Vector3.new(a.X,0,a.Z)
        nang = Vector3.new(nang.X,0,nang.Z)
    end 
    return (nang-a).magnitude
end
local Last
function tpT(t, k, dieukien, disableinstanttp,instanttp)

    if Last then Last() Last=nil end
    if not plr.Character:FindFirstChild("HumanoidRootPart")  or not plr.Character:FindFirstChild("UpperTorso") then return end
    if instanttp then 
        plr.Character.HumanoidRootPart.CFrame=t
        return
    end
    if kc(t.p) > 2000 then 
        plr.Character.HumanoidRootPart.CFrame=t
        return
    end
    if plr.Character:FindFirstChild("HumanoidRootPart") and not disableinstanttp
    and (plr.Character.HumanoidRootPart.Position-t.p).magnitude < 80 then 
        plr.Character.HumanoidRootPart.CFrame=t
    else
        if not k then
            k = 100
        end
        local tween_s = game:service "TweenService"
        local info =
            TweenInfo.new(
            (plr.Character:WaitForChild("HumanoidRootPart").Position - t.p).magnitude / k,
            Enum.EasingStyle.Linear
        )
        local breakdk = false
        local tic_k = tick()
        local cframe
        if plr.Character.UpperTorso:FindFirstChild(rnd) then 
            cframe= CFrame.lookAt(t.Position, plr.Character.UpperTorso[rnd].CFrame.lookVector)
        else
            cframe = CFrame.lookAt(t.Position, plr.Character.HumanoidRootPart.CFrame.lookVector)
        end
        local tween, err =
            pcall(
            function()
                local tween =
                    tween_s:Create(plr.Character:WaitForChild("HumanoidRootPart"), info, {CFrame = cframe})
                local done = false
                local Stop = function() done=true end
                Last=Stop
                tween.Completed:Connect(
                    function()
                        done = true
                    end
                )
                SetEN("Noclip", "Tween", true)
                tween:Play()
                while not done do
                    if not plr.Character:FindFirstChild("HumanoidRootPart") then return end
                    SetEN("Noclip", "Tween", true)
                    if (plr.Character.HumanoidRootPart.Position - Vector3.new(30.017883300781, 68.458869934082, -146.99607849121)).magnitude <= 130
                    and plr.Character.HumanoidRootPart.Position.Y >= 60
                    and plr.Character.HumanoidRootPart.Position.Y < 80 then 
                        tween:Cancel()
                        done=true
                        plr.Character.HumanoidRootPart.CFrame = t
                        break
                    end
                    if  ((plr.Character.HumanoidRootPart.Position-t.p).magnitude < 80 or instanttp) and not disableinstanttp then 
                        tween:Cancel()
                        done=true
                        plr.Character.HumanoidRootPart.CFrame = t
                        break
                    end
                    if dieukien and type(dieukien)=="function" then 
                        if not dieukien() then 
                            tween:Cancel()
                            done=true
                            breakdk=true
                            break;
                        end
                    end
                    wait()
                end
                tween:Cancel()
                SetEN("Noclip", "Tween", false)
            end
        )
        SetEN("Noclip", "Tween", false)
        return breakdk;
    end
end

if not getgenv().DisableClaimHive then 
    while not GetPlrHive() do 
        for _, v in pairs(reverse(game.Workspace.Honeycombs:GetChildren())) do
            if tostring(v.Owner.Value) == "nil" then
                tpT(v.LightHolder.CFrame)
                wait(1)
                game.ReplicatedStorage.Events.ClaimHive:FireServer(v.HiveID.Value)
                break;
            end
        end
    end
end
getfenv().Settings=Settings
function Walkk(t, token,dieukien,spamwalk)
    local Character = plr.Character
    local Humanoid = Character:WaitForChild("Humanoid")
    local stop = false
    Character:WaitForChild("Humanoid"):MoveTo(t.p)
    local vohoangnang = Character:WaitForChild("Humanoid").MoveToFinished:Connect(
        function()
            stop = true
        end
    )
    local a = tick()
    while (stop == false) do
        if Call then
            Call()
        end
        wait()
        if spamwalk then 
            Character:WaitForChild("Humanoid"):MoveTo(t.p)
        end
        if (token and not getgenv().IsToken(token)) then
        Character:WaitForChild("Humanoid"):Move(Vector3.new(0, 0, 0))
            stop=true
            vohoangnang:Disconnect()
            return
        end
        if dieukien and not dieukien() then 
            Character:WaitForChild("Humanoid"):Move(Vector3.new(0, 0, 0))
            stop=true
            vohoangnang:Disconnect()
            return
        end
        if tick() - a >= 5  then
            Character:WaitForChild("Humanoid"):Move(Vector3.new(0, 0, 0))
            plr.Character:WaitForChild("HumanoidRootPart").CFrame = t
            stop = true
        end
    end
    vohoangnang:Disconnect()
end
function WalkPathFind(destination,limittime,CallWhenWalk) 
    --print("Walked Path Find")
    if kc(destination.p,true)<7 then return end
    local PathfindingService = game:GetService("PathfindingService")
    local Players = game:GetService("Players")

    local RunService = game:GetService("RunService")
    
    local path = PathfindingService:CreatePath()
    
    local player = Players.LocalPlayer
    local character = player.Character
    local humanoid = character:WaitForChild("Humanoid")
    
    local TEST_DESTINATION = Vector3.new(100, 0, 100)
    
    local waypoints
    local nextWaypointIndex
    local reachedConnection
    local blockedConnection
    
    local stopeed = false
    local called = false
    local function followPath(destination)
        if stopeed then return end
        -- Compute the path
        local success, errorMessage = pcall(function()
            path:ComputeAsync(character.PrimaryPart.Position, destination.p)
        end)
        
        if success and path.Status == Enum.PathStatus.Success and not stopeed then
            -- Get the path waypoints
            waypoints = path:GetWaypoints()
            -- Detect if path becomes blocked
            blockedConnection = path.Blocked:Connect(function(blockedWaypointIndex)
                -- Check if the obstacle is further down the path
                if blockedWaypointIndex >= nextWaypointIndex then
                    -- Stop detecting path blockage until path is re-computed
                    blockedConnection:Disconnect()
                    -- Call function to re-compute new path
                    if not stopeed then 
                        followPath(destination)
                    end
                end
            end)
    
            -- Detect when movement to next waypoint is complete
            if not reachedConnection then
                reachedConnection = humanoid.MoveToFinished:Connect(function(reached)
                    if nextWaypointIndex and reached and nextWaypointIndex < #waypoints and not stopeed then
                        -- Increase waypoint index and move to next waypoint
                        nextWaypointIndex = nextWaypointIndex+1
                        local oldwaypoint = nextWaypointIndex
                        -- if CallWhenWalk then 
                        --     CallWhenWalk()
                        -- end
                        local c = tick()
                        while oldwaypoint == nextWaypointIndex and nextWaypointIndex < #waypoints and tick()-c < 10 and not stopeed do
                            humanoid:MoveTo(waypoints[nextWaypointIndex].Position)
                            wait(1)
                        end
                    else
                        stopeed = true
                        reachedConnection:Disconnect()
                        blockedConnection:Disconnect()
                    end
                end)
            end
    
            -- Initially move to second waypoint (first waypoint is path start; skip it)

            nextWaypointIndex = 2
            if CallWhenWalk and not stopeed and not called then 
                CallWhenWalk()
                called = true
            end
            humanoid:MoveTo(waypoints[nextWaypointIndex].Position)
        else
            warn("Path not computed!", errorMessage)
        end
    end
    followPath(destination)
    if waypoints then 
        if not limittime then limittime = math.huge end
        local VoHoangNang = tick()
        repeat wait() until nextWaypointIndex>=#waypoints or tick() - VoHoangNang > limittime or stopeed or kc(destination.p,true)<3
        if reachedConnection then reachedConnection:Disconnect()
            end
            if blockedConnection then blockedConnection:Disconnect() end
    end
    stopeed = true
end
function WalkPathFind2(destination,sucvatruabithieunang,CallWhenWalk) 
    print("Walked Path Find")
    local PathfindingService = game:GetService("PathfindingService")
    local Players = game:GetService("Players")
    local RunService = game:GetService("RunService")
    
    local path = PathfindingService:CreatePath()
    
    local player = Players.LocalPlayer
    local character = player.Character
    local humanoid = character:WaitForChild("Humanoid")
    
    local TEST_DESTINATION = Vector3.new(100, 0, 100)
    
    local waypoints
    local nextWaypointIndex
    local reachedConnection
    local blockedConnection
   
    local function followPath(destination)
        -- Compute the path
        local success, errorMessage = pcall(function()
            path:ComputeAsync(character.PrimaryPart.Position, destination.p)
        end)
    
        if success and path.Status == Enum.PathStatus.Success then
            -- Get the path waypoints
            waypoints = path:GetWaypoints()
    
            -- Detect if path becomes blocked
            for k,v in pairs(waypoints) do
                if CallWhenWalk then 
                    CallWhenWalk()
                end
                Walkk(CFrame.new(v.Position),nil,nil,true) end
        else
            warn("Path not computed!", errorMessage)
        end
    end
    followPath(destination)
   -- repeat wait() until nextWaypointIndex>=#waypoints
end
function TpToHive()
    pcall(function() 
        local sp = plr.SpawnPos.Value.p
        local p = CFrame.new(sp.X, sp.Y, sp.Z, -0.996, 0, 0.02, 0, 1, 0, -0.02, 0, -0.9) + Vector3.new(0, 0, 8)
        Going = true
        tpT(p, 100)
        Going = false
    end)
end
function TpToField(Field,dk)
    local p = GetFieldByName(Field).CFrame * CFrame.new(0, 0, 0) + Vector3.new(0, 8, 0)
    return tpT(p, 100,dk)
end
function IsBackPackFull(a)
    if Settings.BaloonMethod ~= "Convert on sell" then 
        if GetHiveBallon(Settings.ConvertAtB or 0) then 
            return true
        end
    end
    
    local bool = false
    local Player = plr
    local Character = Player.Character
    local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
    if not a then a = 100 end
    if Player.CoreStats.Pollen.Value >= (Player.CoreStats.Capacity.Value*a)/100 then
        bool = true
    end
    return bool
end
local choithuoc = tick()
function Dig()
    coroutine.wrap(
        function()
            local tool
            for _, v in pairs(plr.Character:GetChildren()) do
                if v:IsA("Tool") and v:FindFirstChild("ClickEvent") then
                    tool = v
                end
            end
            local s, e =
                pcall(
                function()
                    if tool and getsenv and not is_sirhurt_closure and not PROTOSMASHER_LOADED then -- Sirhurt and proto argggg
                        local t = getsenv(tool.ClientScriptMouse).collectStart
                        t()
                    else
                        if tool then
                        tool.ClickEvent:FireServer()
                        end
                    end
                end
            )
            if e then
                pcall(
                    function()
                        if tool then
                        tool.ClickEvent:FireServer()
                        end
                    end
                )
            end
        end
    )()
    pcall(
        function()
            if tick()-choithuoc<0.2 then 
                workspace.NPCs.Onett.Onett["Porcelain Dipper"].ClickEvent:FireServer()
                choithuoc=tick()
            end            
            --DigOther()
        end
    )
end

loadstring([[
    function IsSprout()
        local Particles = game.Workspace.Particles
        local Folder2 = Particles.Folder2
        for k, v in pairs(Folder2:GetChildren()) do
            if v.Name == "Sprout" then
                return v
            end
        end
        return nil
    end
]])()

function GetNearestFirefly() 
    local gancmnnhat
    for k,v in pairs(game.Workspace.NPCBees:GetChildren()) do 
        if v.Name == "Firefly" then 
            if v:FindFirstChild("BodyVelocity") and v.BodyVelocity.Velocity == Vector3.new(0,0,0) then 
                local tuoidz = GetNerestFieldByObject(v)
                if tuoidz then 
                    local sanghuman = IsValidTokenPos(v,tuoidz)
                    if sanghuman then 
                        if sanghuman < 4 then 
                            if not gancmnnhat then 
                                gancmnnhat = v
                            end
                            if (plr.Character.HumanoidRootPart.Position-v.Position).magnitude < (plr.Character.HumanoidRootPart.Position-gancmnnhat.Position).magnitude then 
                                gancmnnhat = v
                            end
                        end
                    end
                end
            end
        end
    end
    return gancmnnhat
end

function GetCurrenItem(Item)
    local StatCache = TvkStatCache
    local a = StatCache["Eggs"][Item]
    if a then return a else return 0 end
end
function GetCurrenMicro()
    local StatCache = TvkStatCache
    return StatCache["Eggs"]["Micro-Converter"]
end

function IsBuffOn(Buff)
    for k,v in pairs(ListTileGrid) do 
        local PlGui = v
        for k, v in pairs(PlGui:GetChildren()) do
            if v:FindFirstChild("BG") then
                if v.BG:FindFirstChild("Icon") then
                    if string.match(v.BG.Icon.Image, BarId[Buff]) then
                        return true
                    end
                end
            end
        end
    end
    
    return false
end
function GetMemoList()
    local tab = {}
    for k, v in pairs(game.Workspace.Toys:GetChildren()) do
        if string.match(v.Name, "Memory Match") then
            table.insert(tab, v)
        end
    end
    return tab
end

function GetInstantList()
    local tab = {}
    for k, v in pairs(game.Workspace.Toys:GetChildren()) do
        if string.match(v.Name, "Instant Converter") then
            table.insert(tab, v)
        end
    end
    return tab
end
function ObjListTostring(tabl)
    local Tab = {}
    for k, v in pairs(tabl) do
        table.insert(Tab, v.Name)
    end
    return Tab
end
local TFItemHook = ListToOb(GetItemList())

if not Settings.TFItemHook then Settings.TFItemHook=TFItemHook else TFItemHook=Settings.TFItemHook end
function ListToField()
    local ListAll = GetItemListWithValue()
    local fields = {}

    if Settings.WHShowHoney then
        table.insert(
            fields,
            {
                name = "Stats",
                value = "Honey: " .. tostring(formatNumber(plr.CoreStats.Honey.Value))
                .. "\nHoney Made: " .. formatNumber(getgenv().HoneyMade),
                inline = false
            }
        )
    end
    local ItemsValue = ""
    for k, v in pairs(TFItemHook) do
        if v then
            ItemsValue = ItemsValue .. k .. ": " .. tostring(ListAll[k]) .. "\n"
        end
    end
    if ItemsValue~="" then 
        table.insert(
            fields,
            {
                name = "Items",
                value = ItemsValue,
                inline = false
            }
        )
    end
    return fields
end
function CollectAllTokenInField()
    for k, v in pairs(game.Workspace.Collectibles:GetChildren()) do
        if
            getgenv().IsToken(v) and
                getgenv().IsValidTokenPos(v, GetNerestFieldByObject(plr.Character:WaitForChild("HumanoidRootPart")))
         then
            Walkk(
                CFrame.new(
                    v.Position.X,
                    plr.Character:WaitForChild("HumanoidRootPart").Position.Y,
                    v.Position.Z
                )
            )
        end
    end
end
function UseAnt()
    game.ReplicatedStorage.Events.ToyEvent:FireServer("Ant Challenge")
end
function NormalSell()
    local old = TvkStatCache.SessionAccessories.Hat
    if Settings.EquipHoneySell then 
        game:GetService("ReplicatedStorage").Events.ItemPackageEvent:InvokeServer("Equip", {
            ["Mute"] = true,
            ["Type"] = "Honey Mask",
            ["Category"] = "Accessory"
        })
    end
    local Player = plr
    local Character = Player.Character
    local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
    local sangzboi = HumanoidRootPart.CFrame
    TpToHive()
    wait(.2)
    game:GetService("ReplicatedStorage").Events.PlayerHiveCommand:FireServer("ToggleHoneyMaking")
    wait(.5)
    repeat
        local tpos = plr.PlayerGui.ScreenGui.ActivateButton
        if tpos.AbsolutePosition.Y ~= 4 then
            game:GetService("ReplicatedStorage").Events.PlayerHiveCommand:FireServer("ToggleHoneyMaking")
            TpToHive()
            wait(.5)
        end
        if string.match(tpos.TextBox.Text, "Stop") then
        else
            if string.match(tpos.TextBox.Text, "Collect") then
            else
                if string.match(tpos.TextBox.Text, "Talk") then
                else
                    game:GetService("ReplicatedStorage").Events.PlayerHiveCommand:FireServer(
                        "ToggleHoneyMaking"
                    )
                    wait(.5)
                end
            end
        end
        wait()
    until (function() if Settings.ConvertBallon then 
    if GetHiveBallon(Settings.ConvertAtB or 0) then return false end
    end 
    if Player.CoreStats.Pollen.Value <= 0 then return true end
end)() or not Settings.Farm or not Running or not ValidFarm()
    wait(3)
    game:GetService("ReplicatedStorage").Events.ItemPackageEvent:InvokeServer("Equip", {
        ["Mute"] = true,
        ["Type"] = old,
        ["Category"] = "Accessory"
    })
end

function GetValidAntPos() 
    local mid=CFrame.new(93.422752380371, 31.946582794189, 553.12829589844)
    local left=CFrame.new(93.422752380371, 31.946582794189, 553.12829589844)
    local right = CFrame.new(92.35001373291, 31.946582794189, 532.30163574219)

    local tb = {
        mid=CFrame.new(93.422752380371, 31.946582794189, 553.12829589844),
        left=CFrame.new(89.871429443359, 31.946582794189, 571.10089111328),
        right= CFrame.new(86.353813171387, 31.946582794189, 527.67553710938)
    }
    local fk = {}
    for k,v in pairs(tb) do fk[k]=false end
    local has = false
    for i,v in pairs(workspace.Toys["Ant Challenge"].Obstacles:GetChildren()) do
        if v:FindFirstChild("Root") then
            local root = plr.Character:FindFirstChild("HumanoidRootPart")
            if root then 
                if true  then
                    has=true
                    local vpos = v.Root.Position
                    local near,ractvk = nil
                    for k,v in pairs(tb) do 
                        if not ractvk then ractvk = k end
                        if (v.p-vpos).magnitude< (tb[ractvk].p-vpos).magnitude then 
                            --near=v
                            ractvk=k
                        end
                    end
                    if ractvk then 
                        fk[ractvk]=true
                    end
                end
            end
        end
    end
    if has then 
        for k,v in pairs(fk) do 
            if not v then return tb[k] end
        end
    end
    
    return tb["mid"]

end
function CheckNear(pos,mob) 
    for k,v in pairs(game.Workspace.Monsters:GetChildren()) do 
        if string.match(v.Name,mob) then 
            if v:FindFirstChild("Torso") or v:FindFirstChild("HumanoidRootPart") then 
                if ((v:FindFirstChild("Torso") or v:FindFirstChild("HumanoidRootPart")).Position-pos.p).magnitude<20 then 
                    return true
                end
            end
        end
    end
    return false
end
function GetPuffRoomLevel(v) 
--    game:GetService("Workspace").Happenings.Puffshrooms.PuffballMushroomModelCommon["Puffball Top"].Attachment.Gui.NameRow.TextLabel
    local level = 25
    if v:FindFirstChild("Puffball Top") and v["Puffball Top"]:FindFirstChild("Attachment") and  v["Puffball Top"].Attachment:FindFirstChild("Gui") and  v["Puffball Top"].Attachment.Gui:FindFirstChild("NameRow") and v["Puffball Top"].Attachment.Gui:FindFirstChild("NameRow"):FindFirstChild("TextLabel") then 
        while level>0 do 
            if v["Puffball Top"].Attachment.Gui.NameRow.TextLabel.Text:find(tostring(level)) then 
                return level
            end
            level=level-1
        end
    end
    return 0
end

function PiroField(v,f) 

    local Field = Settings.PuffField
    local FieldTf=Field
    for k,v in pairs(v) do 
        if v:FindFirstChild("Puffball Stem") and FieldTf[GetNerestFieldByObject(v["Puffball Stem"])] then 
            return v
        end
    end
    if f then return end

    local Nearest
    for k,v in pairs(v) do 
        if not Nearest and v:FindFirstChild("Puffball Stem") then Nearest=v end
        if plr.Character:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Puffball Stem") then 
            if (plr.Character.HumanoidRootPart.Position-v["Puffball Stem"].Position).magnitude<(plr.Character.HumanoidRootPart.Position-Nearest["Puffball Stem"].Position).magnitude then 
                Nearest=v
            end
        end
    end
    return Nearest
end
function GetCurrentHive() 
    for k,v in ipairs(game:GetService("Workspace").Honeycombs:GetChildren()) do 
        if tostring(v.Owner.Value)==plr.Name then 
            return v
        end
    end
end
loadstring([[
    function GetBallonLevel(v,max) 
        if pcall(function() return v.BalloonBody.GuiAttach.Gui.BlessingBar.TextLabel end) then 
            local text =v.BalloonBody.GuiAttach.Gui.BlessingBar.TextLabel.Text
            for i=1,200 do 
                if text=="🎈 Blessing x"..i then 
                    return i
                end
            end
        end
    end
]])()
function GetHiveBallon(bl)
    local Hive = GetCurrentHive()
    if Hive then 
        for k,v in ipairs(game:GetService("Workspace").Balloons.HiveBalloons:GetChildren()) do 
            if v:FindFirstChild("BalloonRoot") and  pcall(function() return v.BalloonBody.GuiAttach.Gui.BlessingBar.TextLabel end)  then 
                if (v.BalloonRoot.Position - Hive.SpawnPos.Value.p).magnitude<30 then 
                    local lv = (v:FindFirstChild("Level") and v.Level.Value) or GetBallonLevel(v)
                    if lv then 
                        if not v:FindFirstChild("Level") then 
                            local levl = Instance.new("IntValue",v)
                            levl.Name="Level"
                            levl.Value=lv
                        end
                        if v.BalloonBody.GuiAttach.Gui.BlessingBar.TextLabel.Text~="🎈 Blessing x"..v.Level.Value then 
                            v.Level.Value=GetBallonLevel(v)
                        end
                        if lv>=bl then return v end
                    end
                end
            end
        end
    end
end
function GetRaity(puff) 
    for k,v in pairs(PuffRaity) do 
        if string.match(puff.Name,v) then 
            return v
        end
    end
    return "Normal"
end
function GetNearestPushroom(Field)
    local FieldTf = PFieldTF

    -- Mythic > Legendary > Epic > Level 10+ > Rare > Highest Level
    local ListPuff = {}
    for k,v in pairs(game:GetService("Workspace").Happenings.Puffshrooms:GetChildren()) do
        if v:FindFirstChild("Puffball Stem") then 
            local a = GetRaity(v)
            if PuffRaityTF[a] then 
                local lv = GetPuffRoomLevel(v)
                if lv>=Settings.MinPuff and lv<=Settings.MaxPuff then 
                    if FieldTf[GetNerestFieldByObject(v["Puffball Stem"])] then 
                        table.insert(ListPuff,v)
                    end
                end
            end
        end
    end
    table.sort(ListPuff,function(a,b) 
        return a["Puffball Stem"].Position.magnitude < b["Puffball Stem"].Position.magnitude
    end)
    -- Mythic > Legendary > Epic
    local BestRaity = {}
    for k,v in pairs(PuffRaity) do 
        table.insert(BestRaity,v)
    end
    if Settings.PuffRMethod=="Normal > Mythic" then 
        reverse(BestRaity)
    end

    local Check=false
    local ReturnList = {}
    for k,v in pairs(BestRaity) do 
        if TPuffRaityTF[v] then 
            for k2,v2 in pairs(ListPuff) do 
                if string.match(v2.Name,v) then table.insert(ReturnList,v2) Check=true end
            end
            if Check then break end
        end
    end
    if Check then 
        return PiroField(ReturnList)
    end
    -- Piro Field
    local piro = PiroField(ListPuff,true)
    if piro then 
        return piro
    end

    -- Highest
    local Highest
    for k,v in pairs(ListPuff) do 
        if v:FindFirstChild("Puffball Stem") then 
            if not Highest then Highest=v end
            if Settings.LevelMethod == "Priority High Level" then 
                if GetPuffRoomLevel(v)>GetPuffRoomLevel(Highest) then Highest=v end
            else
                if GetPuffRoomLevel(v)<GetPuffRoomLevel(Highest) then Highest=v end
            end
        end
    end
    return Highest
end
function GetSortedBubble(Field)
    local token = {}
    local sortedtoken = {}
    for k, v in pairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part") then
            if v.Name == "Bubble" then
                if getgenv().IsValidTokenPos(v, Field) and ValidFarm() and Settings.Farm then
                    table.insert(token,v)
                end
            end
        end
    end
    

    local function Por(p)
        local nr
        local kk = 0
        for k, v in pairs(token) do
            if not nr then
                nr = v
                kk = k
            end
            
            if (v.Position - p.Position).magnitude < (nr.Position - p.Position).magnitude then
                nr = v
                kk = k
            end
        
        end
        if nr then
            table.insert(sortedtoken, nr)
            table.remove(token, kk)
            Por(nr)
        end
    end
    Por(plr.Character:WaitForChild("HumanoidRootPart"))
    
    return sortedtoken
end
function IsAnyCrosshair(Field) 
    for k, v in pairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("MeshPart") then
            if v.Name == "Crosshair" then
                if getgenv().IsValidTokenPos(v, Field) and (v.Color==Color3.fromRGB(144,119,87) or v.Color==Color3.fromRGB(119, 85, 255)) then
                    return true
                end
            end
        end
    end
end
function GetSortedCrossHair(Field)
    local token = {}
    local sortedtoken = {}

    -- local SortedFire
    -- if  Settings.GatherFlame then SortedFire = GetSortedFire(Field) end 
    for k, v in pairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("MeshPart") then
            if v.Name == "Crosshair" then
                if getgenv().IsValidTokenPos(v, Field) and (v.Color~=Color3.fromRGB(17, 134, 19)) then
                    if false and Settings.GatherFlame then 
                        local tuoidz
                        for k,v2 in pairs(SortedFire) do 
                            if (v2.Position-v.Position).magnitude < 20 then 
                                tuoidz= true
                                break;
                            end
                        end
                        if tuoidz then 
                            if not v:FindFirstChild("Dit me m rua") then 
                                Instance.new("BoolValue",v).Name = "Dit me m rua"
                            end
                            table.insert(sortedtoken,v)
                        else
                            table.insert(token,v)
                        end
                    else
                        table.insert(token,v)
                    end
                end
            end
        end
    end
    

    local function Por(p)
        local nr
        local kk = 0
        for k, v in pairs(token) do
            if not nr then
                nr = v
                kk = k
            end
            
            if (v.Position - p.Position).magnitude < (nr.Position - p.Position).magnitude then
                nr = v
                kk = k
            end
        
        end
        if nr then
            table.insert(sortedtoken, nr)
            table.remove(token, kk)
            Por(nr)
        end
    end
    Por(plr.Character:WaitForChild("HumanoidRootPart"))
    
    return sortedtoken
end
function GetSortedItem(tab,Field)
    if not tab then return end
    local token = {}
    local sortedtoken = {}
    for k, v in pairs(tab) do
        if not v.Activated then 
            v = v.Part
            if v:IsA("MeshPart") then
                if v.Name == "Crosshair" then
                    if getgenv().IsValidTokenPos(v, Field) and ValidFarm() and Settings.Farm then
                        table.insert(token,v)
                    end
                end
            end
        end
        
    end
    

    local function Por(p)
        local nr
        local kk = 0
        for k, v in pairs(token) do
            if not nr then
                nr = v
                kk = k
            end
            
            if (v.Position - p.Position).magnitude < (nr.Position - p.Position).magnitude then
                nr = v
                kk = k
            end
        
        end
        if nr then
            table.insert(sortedtoken, nr)
            table.remove(token, kk)
            Por(nr)
        end
    end
    Por(plr.Character:WaitForChild("HumanoidRootPart"))
    
    return sortedtoken
end
local ListFlames = {}
local ListFlamesNoDark = {}
function AddFlameToList(ListFlames,tvk,k) 
    for k,v in pairs(ListFlames) do 
        if (tvk.Position-k).magnitude < 15 then 
            table.insert(ListFlames[k],tvk)
            return
        end
    end
    ListFlames[tvk.Position] = {v}
end
function RemoveFlameInList(ListFlames,c) 
    for k,v in pairs(ListFlames) do 
        for k,v2 in pairs(v) do 
            if v2==c or not v2.Parent then 
                table.remove(v,table.find(v,v2))
            end
        end
        if #v==0 then ListFlames[k] = nil end
    end
end
game.Workspace.PlayerFlames.ChildAdded:Connect(function(tvk) 
    delay(0,function() 
        if getgenv().TempField and Settings.Farm and Settings.GatherFlame then 
            if IsValidTokenPos(tvk,getgenv().TempField) then 
                AddFlameToList(ListFlames,tvk,k)
            end
        end
        if getgenv().TempField and Settings.Farm then 
            if IsValidTokenPos(tvk,getgenv().TempField) then 
                AddFlameToList(ListFlamesNoDark,tvk,k)
            end
        end
    end)
end)
game.Workspace.PlayerFlames.ChildRemoved:Connect(function(c) 
    RemoveFlameInList(ListFlames,c)
    RemoveFlameInList(ListFlamesNoDark,c)
end)
function GetNearestFlameGroup(ListFlames,DieuKien) 
    local gancmnnhatK
    local gancmnnhatV
    for k,v in pairs(ListFlames) do
        local pass = true
        if DieuKien then 
            for k,v in pairs(v) do 
                if not DieuKien(v) then 
                    table.remove(ListFlames,table.find(ListFlames,v))
                end
            end 
        end
        if #v < 3 then pass = false ListFlames[k] = nil end
        if pass then 
            if not gancmnnhatK or not gancmnnhatV then 
                gancmnnhatK = k
                gancmnnhatV = v
            end
            if kc(k)<kc(gancmnnhatK) then 
                gancmnnhatK = k
                gancmnnhatV = v
            end 
        end
    end
    --if gancmnnhatV then print(#gancmnnhatV) end
    return gancmnnhatV
end
function GetNearestFire(Field,ruabitheiunang)
    local nr
    if plr.Character:FindFirstChild("HumanoidRootPart") then 
        if ruabitheiunang then 
            local nrGroup = GetNearestFlameGroup(ListFlamesNoDark,function(v) 
                if not v:FindFirstChild("PF") then return false end
                if not v.Parent then return false end
                if v.PF.Color == game:GetService("ReplicatedStorage").LocalFX.LocalFlames.DarkFlame.PF then
                    return false 
                end
                return true
            end)
            if nrGroup and nrGroup[1] then 
                return nrGroup[1] 
            end
        else
            if Field then 
                local nrGroup = GetNearestFlameGroup(ListFlames,function(v) 
                    if not v:FindFirstChild("PF") then return false end
                    if not v.Parent then return false end
                    if not IsValidTokenPos(v,Field) then return false end
                    return true
                end)
                if nrGroup and nrGroup[1] then 
                    return nrGroup[1] 
                end
            else
                for k, v in pairs(game.Workspace.PlayerFlames:GetChildren()) do
                    if v:FindFirstChild("PF") then
                        local tuoidz
                        if Field then 
                            if IsValidTokenPos(v,Field) then 
                                if ruabitheiunang then 
                                    if v.PF.Color ~= game:GetService("ReplicatedStorage").LocalFX.LocalFlames.DarkFlame.PF then 
                                        tuoidz = true
                                    end
                                else
                                    tuoidz=true
                                end
                            end
                        else
                            if ruabitheiunang then 
                                if v.PF.Color ~= game:GetService("ReplicatedStorage").LocalFX.LocalFlames.DarkFlame.PF then 
                                    tuoidz = true
                                end
                            else
                                tuoidz=true
                            end
                        end
                        if tuoidz then
                            if not nr then 
                                nr=v
                            end
                            if (plr.Character.HumanoidRootPart.Position-v.Position).magnitude < (plr.Character.HumanoidRootPart.Position-nr.Position).magnitude then 
                                nr=v
                            end
                        end
                    end
                end
            end
        end
    end
    return nr
end
function GetListFire(Field) 
    local ListFire = {}
    -- for k, v in pairs(game.Workspace.PlayerFlames:GetChildren()) do
    --     if v:FindFirstChild("PF") then
    --         local tuoidz
    --         if Field then 
    --             if IsValidTokenPos(v,Field) then tuoidz = true end
    --         else
    --             tuoidz=true
    --         end
    --         if tuoidz then
    --             table.insert(ListFire,v)
    --         end
    --     end
    -- end
    for k,v in pairs(ListFlames) do 
        table.insert(ListFire,{Position = k})
    end
    return ListFire
end
function GetSortedFire(Field) 
    local ListFire = {}
    -- for k, v in pairs(game.Workspace.PlayerFlames:GetChildren()) do
    --     if v:FindFirstChild("PF") then
    --         local tuoidz
    --         if Field then 
    --             if IsValidTokenPos(v,Field) then tuoidz = true end
    --         else
    --             tuoidz=true
    --         end
    --         if tuoidz then
    --             table.insert(ListFire,v)
    --         end
    --     end
    -- end
    for k,v in pairs(ListFlames) do 
        table.insert(ListFire,{Position = k})
    end
    table.sort(ListFire,function(a,b) 
        return kc(a.Position)<kc(b.Position)
    end)
    return ListFire
end
function GetNearestDupe(Field) 
    local nr
    if plr.Character:FindFirstChild("HumanoidRootPart") then 
        for k, v in pairs(game:GetService("Workspace").Camera.DupedTokens:GetChildren()) do
            if IsToken(v) and getgenv().IsValidTokenPos(v,Field) and not IsTokenBlacklist(v) then
                if string.match(v.FrontDecal.Texture,"5877939956") then return v end
                if not nr then 
                    nr=v
                end
                if (plr.Character.HumanoidRootPart.Position-v.Position).magnitude < (plr.Character.HumanoidRootPart.Position-nr.Position).magnitude then 
                    nr=v
                end
            end
        end
    end
    return nr
end
function GetSortedFlame(Field)
    local token = {}
    local sortedtoken = {}
    for k, v in pairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part") then
            if v.Name == "FlamePart" then
                if
                    getgenv().IsValidTokenPos(v, Field) and ValidFarm() and
                        v:FindFirstChild("Fire") and
                        Settings.Farm
                 then
                  table.insert(token,v)
                end
            end
        end
    end
    

    local function Por(p)
        local nr
        local kk = 0
        for k, v in pairs(token) do
            if not nr then
                nr = v
                kk = k
            end
            
            if (v.Position - p.Position).magnitude < (nr.Position - p.Position).magnitude then
                nr = v
                kk = k
            end
        
        end
        if nr then
            table.insert(sortedtoken, nr)
            table.remove(token, kk)
            Por(nr)
        end
    end
    Por(plr.Character:WaitForChild("HumanoidRootPart"))

    return sortedtoken
end

function GetLowestTrans(x)
    local low = math.huge
    local index
    for i, v in pairs(x) do
        if v.Transparency < low then
            low = v.Transparency
            index = i
        end
    end
    return index
end
function GetNearestCoco(x)
    local dist = math.huge
    local index
    for i, v in pairs(x) do
        local magnitude = (v.Position - plr.Character.HumanoidRootPart.Position).magnitude
        if magnitude < dist then
            dist = magnitude
            index = v
        end
    end
    return index
end
local CollectThings = {
    Shower = {},
    Coco = {},
    Metor = {}
}
local ListTr = {}

local rac = game:GetService("ReplicatedStorage").Events.LocalFX
rac.OnClientEvent:Connect(function(...) 
    if Settings.SmartTr then 
        local cac,rac = ...
        if cac=="Triangulate" then
            if plr.Character:FindFirstChild("HumanoidRootPart") then 
                if rac.Part1==plr.Character.HumanoidRootPart then 
                    table.insert(ListTr,{Start = tick(),Obj = rac})
                end
            end
        end
    else
        while #ListTr>0 do 
            table.remove(ListTr,1)
        end
    end

    if Settings.AutoFarmMetor then 
        local suc,vat,rua,thieu,nang = ...
        if suc == "MythicMeteor" then 
            table.insert(CollectThings.Metor,{Start=tick(),Obj = vat})
        end
    end
    for k,v in pairs(CollectThings.Metor) do 
        local delay = v.Obj.Delay or 2.5     
        local tuoidz = v.Obj.Dur or 0.8
        if (tick() > (tuoidz+v.Start+delay)) then 
            table.remove(CollectThings.Metor,table.find(CollectThings.Metor,v))
        end
    end

end)


game.Workspace.Particles.ChildAdded:Connect(function(v) 
    if v.Name=="WarningDisk" then 
        if v.Size.X==30 then 
            table.insert(CollectThings.Coco,v) 
        elseif v.Size.X==8 then
            table.insert(CollectThings.Shower,v) 
        end    
    end
end)

game.Workspace.Particles.ChildRemoved:Connect(function(v) 
    local type
    if v.Name=="WarningDisk" then 
        if v.Size.X==30 then 
            type="Coco"
        elseif v.Size.X==8 then
            type="Shower"
        end    
    end
    if type then 
        for k,val in pairs(CollectThings[type]) do 
            if val==v then table.remove(CollectThings[type],k) end
        end
    end
end)

function GetSortedCoconut(Field, IsShower)
    local type="Coco"
    if IsShower then 
        type="Shower"
    end
    local coco = {}
    local cac = 1
    if Settings.ShowerTP then cac = 0.5 end
    for k,v in pairs(CollectThings[type]) do 
        if plr.Character:FindFirstChild("HumanoidRootPart") and (v.Position-plr.Character.HumanoidRootPart.Position).magnitude<80
        and v:FindFirstChild("Mesh")
        then
            table.insert(coco,v)
        end
    end
    return coco;
end

function GetNearestBalloon(Field) 
    local nrs 
    for k,v in pairs(game:GetService("Workspace").Balloons.FieldBalloons:GetChildren()) do 
        if v:FindFirstChild("PlayerName") then 
            if v.PlayerName.Value==plr.Name then 
                if v:FindFirstChild("BalloonRoot") then 
                    if IsValidTokenPos(v.BalloonRoot,Field) then
                        if plr.Character:FindFirstChild("HumanoidRootPart") then 
                            if not nrs then 
                                nrs = v
                            end
                            if (plr.Character.HumanoidRootPart.Position-v.BalloonRoot.Position).magnitude<(plr.Character.HumanoidRootPart.Position-nrs.BalloonRoot.Position).magnitude then 
                                nrs = v
                            end
                        end
                    end
                end 
            end
        end
    end
    return nrs
end

function GetMark(Field)
    local dist = math.huge
    local mark
    for k, v in ipairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part")
        and v.Name == "AreaRing"
        and getgenv().IsValidTokenPos(v, Field) then
            if ValidFarm()
            and Settings.Farm then
                local magnitude = (v.Position - plr.Character.HumanoidRootPart.Position).magnitude
                if magnitude < dist then
                    dist = magnitude
                    mark = v
                end
            end
        end
    end
    return mark
end




function GetBallon()
    for k, v in ipairs(game.Workspace.Particles:GetChildren()) do
        if v:IsA("Part")
        and v.Name == "AreaRing" then
            if ValidFarm()
            and Settings.Farm then
                return v
            end
        end
    end
end
-- getgenv().PrioritizeList = PrioritizeList
-- getgenv().IgnoreListTF = IgnoreListTF
-- function SetupHookIgnore() 
--     local cache = {}

--     local rm = game:GetService("ReplicatedStorage").Events.CollectibleEvent
--     for k,v in pairs(getconnections(rm.OnClientEvent)) do
--         local oldHookIgnore
--         oldHookIgnore = hookfunction(v.Function,function(...) 
--             local a,p = ...
--             if a=="Spawn" and p and p.Icon then 
--                 for k,val in pairs(getgenv().PrioritizeList) do
--                     if getgenv().IgnoreListTF[k] and string.match(p.Icon, val) then
--                         return
--                     end
--                 end
--             end
--             return oldHookIgnore(...)
--         end)
--     end
-- end
-- SetupHookIgnore()
function SetupTokenFolder(TokenFolder,ListAllToken) 
    local TokenIdCache = {}

    TokenFolder.ChildAdded:Connect(function(v)
        local field = GetNerestFieldByObject(v)
        if not ListAllToken[field] then 
            ListAllToken[field]={}
        end
        local Token
        if v:FindFirstChild("FrontDecal") then
            local Piro = TokenIdCache[v.FrontDecal.Texture]
            if not Piro then 
                for k,val in pairs(PrioritizeList) do
                    if string.match(v.FrontDecal.Texture,val) then
                        TokenIdCache[v.FrontDecal.Texture] = k
                        if PrioritizeListTF[k] then
                            Token=k
                            break; 
                        end
                        if IgnoreListTF[k] and string.match(v.FrontDecal.Texture, val) then
                            --delay(0,function() v:Destroy() end)
                            return
                        end
                    end
                end
            else
                if PrioritizeListTF[Piro] then Token = v end
                if IgnoreListTF[Piro] then return end
            end
            
        end
        if Token then 
            if not ListAllToken[field][Token] then 
                ListAllToken[field][Token]={}
            end
            table.insert(ListAllToken[field][Token],v)     
        else
            if not ListAllToken[field]["None"] then 
                ListAllToken[field]["None"]={}
            end
            table.insert(ListAllToken[field]["None"],v)    
        end
    end)

    TokenFolder.ChildRemoved:Connect(function(v) 
        local field = GetNerestFieldByObject(v)
        if not ListAllToken[field] then 
            ListAllToken[field]={}
        end
        local index=0
        for k,val in pairs(ListAllToken[field]) do 
            for k,val2 in pairs(val) do 
                if val2==v then 
                    table.remove(val,k)
                    break;
                end
            end
        end
    end)
end

SetupTokenFolder(game.Workspace.Collectibles,ListAllToken)
SetupTokenFolder(game:GetService("Workspace").Camera.DupedTokens,ListAllDupedToken)

-- function CountTabT(ListAllToken) 
--     local c = 0
--     for k,val in pairs(ListAllToken) do
--         for k,val in pairs(val) do 
--             for k,val2 in pairs(val) do 
--                 c=c+1
--             end
--         end
--     end
--     return c
-- end

local ks = {}
for k, v in pairs(GetInstantList()) do
    ks[v.Name] = v.Platform.CFrame
end

local ListBuff = {"Blue Extract", "Red Extract", "Oil", "Enzymes", "Glue", "Tropical Drink", "Stinger","Glitter", "Magic Bean"}
local ListFieldBoost = {"Red Field Booster", "Blue Field Booster", "Field Booster", "Coconut Dispenser"}
local TFListFieldBoost = ListToOb(ListFieldBoost, false)
TFListFieldBoost["[Setting] Only enable when theres no boost"] = false
local FarmBuffList = {
    ["Blue Extract"] = false,
    ["Red Extract"] = false,
    ["Oil"] = false,
    ["Enzymes"] = false,
    ["Glue"] = false,
    ["Tropical Drink"] = false,
    ["Stinger"] = false,
    ["Glitter"] = false,
    ["Magic Bean"] = false
}

FarmBuffList = SetupTFNor(FarmBuffList,"FarmBuffList")
if not Settings.TFListFieldBoost then Settings.TFListFieldBoost = TFListFieldBoost else TFListFieldBoost=Settings.TFListFieldBoost end



local CurrentField = "Sunflower Field"
local Field = CurrentField
local TempField = Field

local LevelFarmVK = vToK(LevelFarm)
local FarmFieldList = setmetatable({},{
    __index = function(self,index)
        if LevelFarmVK[index]==0 then return end
        return self[LevelFarm[LevelFarmVK[index]-1]]
    end
}) 
FarmFieldList["CurrentField"] = Settings.CurrentField or "Sunflower Field"


getgenv().isActiveTokens = function(v)
    if v and v:IsA("Part") then
        return not ((v.Transparency + 0.05) > 0.7 and (v.Transparency - 0.05) < 0.7)
    end
end
local ChangeGlider=false
Settings.Glider="Glider"
local t = require(game:GetService("ReplicatedStorage").Parachutes)
local old = t.Get
t.Get = function(a)
    if Settings.ChangeGlider then
        return old(Settings.Glider)
    end
    return old(a)
end



-- UI LIB --# test-sea-hub

# Sephiria Charm Picker（商店自选神器）v1.0.1 — 安装说明

商店里用蓝宝石刷新商品列表的那个按钮旁边，会多出一个**「自选」按钮**。点开它，可以从
**当前这一局可能出现的全部神器 / 石板**里直接挑一个，放进商店的补货栏位 —— **不花蓝宝石**。

放进去之后，那个栏位里的东西**还是要照常用金币买**（价格是游戏自己算的，mod 没碰）。
也就是说：mod 帮你换掉了"这一格卖什么"，没帮你免单，也没改掉落、概率或价格。

- 候选池**照抄游戏自己的过滤规则**（能不能作为奖励、当前职业/武器是否被禁用、类型闸、
  独特效果是否已有、双持组合闸门等），所以你在面板里看到的，就是游戏本来可能刷出来的那些。
- 单机 / 联机都可用。面板与候选池都是**本机计算**的，不走网络，不影响其他玩家。
- 不依赖其他 mod，不改动存档或游戏文件。

---

## 一、怎么用

1. 进商店，在刷新按钮附近点**「自选」**（默认在它下方）。
2. 面板左边是**当前补货栏位**，右边是**候选网格**，顶上一条是**分类标签**。
3. 直接点右边任意一个候选 ⇒ 它会被写进一个栏位（没有空位时会新建一个）。
   想**改已经放好的那一格**：先点左边那张卡片选中它，再点右边的候选覆盖。
4. 关掉面板，商店里那一格就变成你选的东西，照常花金币买下。

细节：

- 面板有**神器 / 石板**两个页签，互不干扰。
- 标签行有「全部」，还有**「无属性」**——有些神器没有任何分类标签，只能在「全部」里看到，
  单独给它们做了一个标签，池子里确实存在这类神器时它才会出现。
- **按 Esc 可以关闭面板**（可在配置里关掉），并且**只关面板**：商店和背包都会留在原处，
  不会跟着一起关。
- 打开商店和打开面板时**都不会凭空造出神器**：必须你点了某个候选，才会创建/写入栏位。
- 已经买掉的那一格会被锁住，剩下的格子仍可继续换。

---

## 二、前置条件：需要 BepInEx 6

本 mod 是 BepInEx 插件，**必须先装好 BepInEx 6（Unity Mono / x64）**。

怎么判断：打开游戏根目录（Steam 里右键 Sephiria → 管理 → 浏览本地文件），
如果同时看到下面这些，说明已经装好了，直接跳到第三节：

```text
Sephiria.exe
winhttp.dll
doorstop_config.ini
BepInEx/
```

> 如果你装过 **Sephiria Together**（联机 mod）的 `with-BepInEx` 整合包，BepInEx 已经自带了。

如果没装：取 **v6 的 Unity Mono x64 构建**（本游戏是 `BepInEx 6.0.0-be.697`，Unity 6000.3.x），
把包里的文件**直接解压到游戏根目录**，让 `winhttp.dll` 和 `Sephiria.exe` 在同一层，
然后**先启动一次游戏**让它生成自己的目录，退出后再装本 mod。

---

## 三、安装

1. Steam 右键 **Sephiria** → **管理** → **浏览本地文件**，打开游戏根目录。
2. 把本压缩包里的 **`BepInEx` 文件夹整个拖进游戏根目录**，和已有的 `BepInEx` 合并。
3. 确认最终路径长这样：

```text
Sephiria/
└─ BepInEx/
   ├─ plugins/
   │  └─ SephiriaCharmPicker.dll       ← 本体
   └─ config/
      └─ com.sephiria.charmpicker.cfg  ← 配置（可选，首次启动会自动生成）
```

4. **重启游戏**（mod 只在启动时加载，热替换无效），进商店看刷新按钮旁边有没有多一个按钮。

> **不要把整个 zip 放进 `BepInEx/plugins`**，也不要放进 `Sephiria_Data`。
> 只要 `SephiriaCharmPicker.dll` 这一个文件在 `BepInEx/plugins/` 下就行。

配置文件可选：不放也会在首次启动时自动生成一份带注释的默认值，
压缩包里这份只是方便你先改好再启动。
**升级时如果沿用旧 cfg，改过默认值的项不会被自动套用** —— 想拿新默认值就删掉旧 cfg 再启动一次。

---

## 四、卸载

删掉这一个文件即可：

```text
Sephiria/BepInEx/plugins/SephiriaCharmPicker.dll
```

配置文件 `Sephiria/BepInEx/config/com.sephiria.charmpicker.cfg` 留着无害，想彻底清理就一起删。
已经买下的东西不受影响。

---

## 五、配置

配置文件：`Sephiria/BepInEx/config/com.sephiria.charmpicker.cfg`
（记事本/VSCode 打开，改完**重启游戏**生效；**游戏开着时改会被覆盖**，请先退出游戏再改）

| 分区 | 配置项 | 默认 | 作用 |
|---|---|---|---|
| General | `Enabled` | `true` | 总开关。关掉后自选按钮被移除、面板不再工作，游戏自己的刷新按钮不受任何影响 |
| General | `DebugLog` | `false` | 每次刷新、每次打开面板都把完整候选列表（名字/稀有度/价格）打进日志。很吵，只在排错时开 |
| Button | `Label` | `自选` | 按钮上的文字，随便填什么都可以 |
| Button | `Placement` | `Down` | 按钮放在刷新按钮的哪一侧：`Left` / `Right` / `Up` / `Down` |
| Button | `Gap` | `8` | 与刷新按钮之间隔多少像素 |
| Button | `OffsetX` / `OffsetY` | `0` | 摆好之后再微调，正数是右 / 上 |
| Button | `DrawOnTop` | `true` | 画在同级按钮之上，免得被商店里别的东西盖住 |
| Button | `Look` | `Solid` | 克隆出来的按钮怎么处理 inherited 图案：`Solid` 隐藏原按钮上的「?」图标和宝石；`Keep` 原样保留 |
| Panel | `AllowCreateSlots` | `true` | 允许在点候选时**新建**补货栏位（不花蓝宝石）。关掉后，自选只能给"已经刷出来的栏位"换东西 |
| Panel | `Parent` | `Journal` | 面板挂在哪个 UI 根下：`Journal`（图鉴那个根，沿用它的缩放与排序）或 `Shop`（商店面板的根）。面板看不见时翻这个值试试 |
| Panel | `SlotWidth` | `0` | 左边栏位列的宽度，`0` = 自动取物品框内宽的约四分之一 |
| Panel | `SlotRows` | `2` | 左列至少要能放下几张卡，卡片据此缩放，永远待在框内 |
| Panel | `FilterBar` | `true` | 是否显示顶部分类标签行 |
| Panel | `FilterMaxRows` | `3` | 标签最多占几行。放不下时会自动缩小字号，不会挤成一团也不会丢标签 |
| Panel | `CloseWithEscape` | `true` | 允许用 Esc 关闭面板 |
| Panel | `FallbackClickHitTest` | `true` | 兜底点击：万一游戏的点击派发这一次谁都没交给（`hits=0`），面板就用自己算出的格子位置接管这次点击。关掉它就完全只听游戏派发 |

---

## 六、排错

本 mod 的所有日志**都在** `Sephiria/BepInEx/LogOutput.log` 里，前缀是 `[SCP]`。

**完全没反应 / 商店里没有多出按钮**

1. 确认 `SephiriaCharmPicker.dll` 在 `BepInEx/plugins/` 下（不是在某个子文件夹里），
   并且**已经重启过游戏**。
2. 在 `LogOutput.log` 里搜 `[SCP] loaded`，正常会有这样一行：

   ```text
   [SCP] loaded v1.0.1 assembly=c57a0daeab8e (baseline c57a0daeab8e) enabled=1 label=自选 place=Down ...
   ```

   - **`assembly=` 后面六个字符和上面不一样** = 游戏版本与 mod 编译时不一致，把这行发我。
   - 有 `could not apply patch class ...` = 补丁没挂上，把那行发我。
   - **一行 `[SCP]` 都没有** = dll 根本没被加载（多半是没重启，或 BepInEx 不是 v6）。

**面板能打开，但点右边的候选没反应**

点一下，然后去日志里找这一行：

```text
[SCP] click: pos=718,642 hits=5[0=*Content/SCP_Cell2033/Icon ...] topIsMine=1 cell0(... raycast=3)
```

- `hits=0` ⇒ **这一次点击，游戏的派发链谁都没交给**。面板会用自己的命中判定接管（同一行末尾
  出现 `fallback=id1234`，并且后面有一条 `cell click id=1234`）；如果接管也没命中
  （`fallback=no`），那才是真的点在空白处。
- `topIsMine=0` ⇒ **点到了别的东西上**（被别的界面盖住了）。后面那条
  `click: the press did not land on the picker panel` 会一起出现，把两行都发我。
  注意：真被盖住时兜底**不会**插手（`fallback=left-to-game`），不会抢游戏界面的点击。
- 有 `cell click id=...` 但接下来是 `pick refused` ⇒ 这一类已经没有可写的栏位了，
  日志里会写明原因。
- 配置里 `FallbackClickHitTest = false` 会关掉上面的接管，只保留游戏自己的派发。

**面板是空的**

看 `[SCP] panel: grid ... cells=` 的数字：`cells=0` 说明候选池是空的（通常是这一局
确实没有符合条件的物品），把 `[SCP] panel: open` 那一行发我。

**候选里没有我想要的那件**

候选池严格照抄游戏自己的过滤规则，所以"游戏本来就不可能在这一格刷出它"的情况，
mod 也不会给。可以开 `DebugLog` 看池子到底是怎么筛的。

---

## 七、English (quick version)

**What it does:** adds an extra **"pick"** button next to the shop's sapphire restock button. It
opens a panel listing every charm / stone tablet that could appear in the current run; picking one
writes it into a restock slot **without spending sapphires**. The item still has to be bought with
gold at its normal, game-computed price — the mod changes *what* is offered, not the price, the
drop rates or the odds.

The candidate pool copies the game's own filters (reward eligibility, class/weapon gating, type
gates, unique-effect ownership, dual-wield combinations), so what you see is what the game could
have rolled anyway. The panel and the pool are computed locally; nothing is sent over the network
and other players are unaffected. Works in single player and multiplayer.

**Install:** BepInEx 6 (Unity Mono, x64) must already be installed. Drag the `BepInEx` folder from
this archive into the game root so the file ends up at `Sephiria/BepInEx/plugins/SephiriaCharmPicker.dll`,
then **restart the game**. Do not put the whole ZIP inside `BepInEx/plugins`, and do not put
anything into `Sephiria_Data`.

**Uninstall:** delete `SephiriaCharmPicker.dll`.

**Config:** `Sephiria/BepInEx/config/com.sephiria.charmpicker.cfg` (auto-generated on first launch if
absent). Edit with the game closed, then restart. BepInEx does not overwrite values already present
in the file, so after an upgrade delete the cfg to pick up new defaults.

Main knobs: `Enabled`, `DebugLog`, `Label`, `Placement` / `Gap` / `OffsetX` / `OffsetY` / `DrawOnTop`
(button look and position), `Look` (`Solid` hides the cloned "?" icon and gem, `Keep` leaves the
game's artwork), `AllowCreateSlots` (create slots when you pick, at no sapphire cost), `Parent`
(`Journal` / `Shop`), `SlotWidth`, `SlotRows`, `FilterBar`, `FilterMaxRows`, `CloseWithEscape`,
`FallbackClickHitTest` (take the click from the panel's own hit test when the game's raycast hands
it to nobody).

**Behaviour worth knowing:** Escape closes the picker panel **only** — the shop and the inventory
panel stay open.

**Behaviour worth knowing:** opening the shop or the panel never creates items on its own — a slot
is created only when you actually click a candidate. Clicking a slot card first selects it, so the
next candidate overwrites that one instead of filling a new one. A slot that has been bought is
locked; the rest stay changeable. There is an "all" tag plus a "no category" tag for charms that
carry no category at all (it only appears when such charms are in the pool).

**Troubleshooting:** everything is logged to `Sephiria/BepInEx/LogOutput.log` with the `[SCP]` prefix.
Look for `[SCP] loaded v1.0.1 assembly=...` first. If the panel opens but clicking a candidate does
nothing, find the `[SCP] click: pos=... hits=N ... topIsMine=...` line: `hits=0` means the press was
handed to nobody, so the panel takes it from its own hit test (the line ends with `fallback=id1234`
and a `cell click id=1234` follows); `fallback=no` means you really pressed empty space.
`topIsMine=0` means something else is covering the panel — the fallback stays out of that case
(`fallback=left-to-game`) and never steals another window's click.

---

## 版本记录 / Changelog

### v1.0.1

- **修掉"当主机时面板错位"**：内容区（标签行、槽位列、卡片大小）的基准是从克隆体的滚动视口
  量出来的；当主机时克隆体醒得更慢，量到的顶边会矮一截，于是整个内容区被压低约 212 像素
  （标签行上方多出一段空白、卡片变矮、底部一行被裁）。现在发现顶边异常就改用目录矩形反推，
  第一把当主机也有效。
- **Esc 只关面板**：以前按 Esc 会把商店一起关掉（同一次按键被两层界面各消费一次），修好后又
  变成背包被关（背包自己重载了关闭逻辑）。现在自选页应答 Esc 期间整个跳过游戏的 Esc 扫描，
  商店和背包都留在原处；万一有漏网的，半秒内会自动把背包重新打开。
- **点击兜底**：有时候游戏的点击派发这一次谁都没交给（日志 `hits=0`），面板就用自己算出的
  格子位置接管这次点击；真被别的界面盖住时不会插手。可用 `FallbackClickHitTest` 关掉。

### v1.0.0

- 首个发布版本：商店「自选」按钮、候选池照抄游戏过滤规则、逐槽冻结、神器 / 石板双页签、
  无属性标签、Esc 关闭面板。

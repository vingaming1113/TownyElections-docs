---
icon: wrench
---

# 配置

`config.yml` 提供了許多選項，可以自訂你的伺服器行為，例如設置選舉系統。

在配置檔案中，你可以找到許多設定。這些設定在配置檔案中都有詳細的說明。

你可以在下方看到完整的預設配置：

```yml
# ============================================================================
#  TownyElections - 配置
# ============================================================================
#  一個正式的、可配置的 Towny 城鎮選舉系統。
#  文件 & 支持：請查看 README.md
# ============================================================================

# 請勿編輯。用於在更新時遷移配置。
config-version: 1

# 一般插件設定。
general:
  # 訊息檔案的語言 (messages_<locale>.yml)。預設為 "en"。
  locale: "en"
  # 如果為 true，會在控制台中記錄額外的除錯資訊。
  debug: false
  # 透過 bStats (https://bstats.org) 啟用匿名使用統計。
  metrics: true

# ----------------------------------------------------------------------------
#  更新檢查
# ----------------------------------------------------------------------------
# 在啟動時，TownyElections 可以檢查 GitHub Releases 是否有更新的穩定版本
# （beta 和 alpha 版本會被忽略）。檢查是非同步執行的，不會阻塞伺服器；
# 它只會記錄到控制台，並且可選擇在管理員進入時通知他們。
# 它永遠不會下載或安裝任何東西。
update-checker:
  # GitHub Releases 更新檢查的主開關。
  enabled: true
  # GitHub 存儲庫，格式為 owner/name。
  github-repository: "vingaming1113/TownyElections"
  # 當管理員進入伺服器時，如果有更新，通知他們。
  notify-admins-on-join: true

# ----------------------------------------------------------------------------
#  選舉設定
# ----------------------------------------------------------------------------
election:
  # 提名/競選階段的持續時間，期間居民可以註冊為候選人。
  # 接受的格式：30s, 10m, 2h, 3d, 1w。
  nomination-duration: "2d"

  # 提名結束後，投票階段的持續時間。
  voting-duration: "3d"

  # 選舉進行到投票階段所需的最低候選人數。
  # 如果註冊的候選人數量少於此數值，選舉將被取消（或自動獲勝，參見 "auto-win-single-candidate"）。
  min-candidates: 2

  # 每次選舉允許的最大候選人數。0 = 不限制。
  max-candidates: 0

  # 如果只有一個候選人註冊，且 min-candidates 會導致選舉失敗，該候選人是否自動獲勝？
  auto-win-single-candidate: true

  # 城鎮舉行選舉前必須擁有的最低居民人數。
  min-town-residents: 2

  # 每位居民在每次選舉中可以投出的票數（通常是 1）。
  votes-per-resident: 1

  # 如果為 true，玩家可以在投票階段開放時更改他們的投票。
  allow-vote-changes: true

  # 如果為 true，居民可以在投票期間看到實時投票統計。如果為 false，統計將隱藏，直到選舉結束（秘密投票）。
  public-live-results: true

  # 候選人可以為自己投票嗎？
  allow-self-vote: false

  # 用於收集和統計選票的選舉系統：
  #   PLURALITY - 每個投票者選擇一位候選人；得票最多者獲勝
  #   RANKED_CHOICE - 投票者按偏好順序排列候選人
  #                   (/election vote First Second Third ...)。計票時執行
  #                   即時淘汰輪次：最弱的候選人被淘汰，他們的選票轉移到每個投票者的
  #                   下一個偏好，直到有人獲得多數票。
  #   APPROVAL - 投票者可以批准任意數量的候選人
  #              (/election vote Alice Bob ...); 得到最多批准的候選人獲勝
  # 選舉開始後，選舉系統就會被鎖定；更改此值不會重新解釋已經進行中的選舉的選票。
  voting-system: "PLURALITY"

  # 當前幾名候選人並列時的平局破解策略：
  #   RANDOM - 從並列的候選人中隨機選擇一位獲勝者
  #   EARLIEST - 最先註冊的候選人獲勝
  #   INCUMBENT - 如果現任鎮長並列，則現任鎮長獲勝，否則 RANDOM
  #   RUNOFF - 在並列的候選人之間開始新的短期投票輪次
  #   NONE - 宣佈沒有獲勝者（選舉無效）
  tie-breaker: "RUNOFF"

  # 平局投票輪次的持續時間（僅在 tie-breaker 為 RUNOFF 时使用）。
  runoff-duration: "1d"

  # 自動在每個符合條件的城鎮中定期開始新的選舉。
  # 將 enabled 設置為 false 以僅手動通過命令運行選舉。
  auto-schedule:
    enabled: true
    # 兩次選舉之間的間隔（每個城鎮）。例如：30d 表示每月一次。
    interval: "14d"

  # 如果為 true，城鎮的經濟賬戶將被收取/獎勵處理（需要經濟插件）。純粹可選的額外功能。
  economy:
    # 居民註冊為候選人的費用。0 = 免費。
    candidacy-cost: 10.0
    # 獲勝者獲得的獎勵（從無到有）。0 = 禁用。
    winner-reward: 500.0

  # 每個 IP 的投票限制，以防止小號濫用。啟用後，每個指紋（IP）可以獲得一張選票，最多配置的指紋數量。
  # IP 地址會被哈希（SHA-256）；只有哈希和投票者的 UUID 會被保存，因此在伺服器重新啟動後，保護仍然有效。
  ip-vote-limit:
    # 每個 IP 投票限制的主開關。false = 禁用（當前行為）。
    enabled: false
    # 在一次選舉中允許的不同 IP 指紋的最大投票數。
    # 0 = 不限制（即使 enabled: true 也會有效禁用）。
    max-votes: 0

# ----------------------------------------------------------------------------
#  競選設定
# ----------------------------------------------------------------------------
campaign:
  # 候選人競選訊息的最大長度（字元）。
  max-message-length: 128
  # 候選人未設置時使用的預設競選訊息。
  default-message: "I would be honored to serve this town."
  # 使用 /election party 輸入的政黨名稱的最大長度（字元）。
  # 這可以保護聊天輸出和 Tab 鍵補全免受非常長的標籤影響。
  max-party-name-length: 32
  # 候選人選擇之前顯示的預設政黨。
  # 這是玩家使用 /election party leave 時返回的政黨。
  default-party-name: "Independent"
  # 如果為 true，預設政黨將隱藏在 /election parties 和政黨結果摘要中。
  # 候選人仍然在候選人列表中保留該標籤。
  hide-default-party-from-standings: false
  # 在一次進行中的選舉中可以存在的非預設政黨的最大數量。
  # 0 = 不限制。這僅限制創建全新的政黨標籤；玩家仍然可以加入已經存在的政黨或離開回到預設政黨。
  max-parties: 0
  # 如果為 true，候選人不能在投票階段開始後更改他們的競選訊息、個人資料、政黨或政黨顏色。
  # 這些只能在提名階段期間編輯。將其設置為 false 以允許在任何時候編輯。
  lock-edits-during-voting: true

  # 一個簡單的拒絕名單。包含這些（不區分大小寫）子字串的競選訊息將被拒絕。
  blocked-words:
    - "slur1"
    - "slur2"

# ----------------------------------------------------------------------------
#  獲勝者獎勵 - 當選候選人獲得的獎勵
# ----------------------------------------------------------------------------
# 當選舉結束時，獲勝者將被授予配置的 Towny 城鎮等級和（可選）成為鎮長。
# 等級必須存在於 Towny 的 townyperms.yml 中（預設包括：helper, councillor, sheriff, treasurer 等，以及你自定義的等級）。
# 無效的等級將被跳過，並顯示控制台警告。
winner:
  # 使獲勝候選人成為城鎮的鎮長。這將轉移鎮長身份。
  set-as-mayor: true

  # 授予城鎮選舉獲勝者的 Towny 城鎮等級。這些映射到 Towny 的 townyperms.yml 中定義的權限節點（例如，地皮管理）。
  grant-town-ranks:
    - "assistant"

  # 如果為 true，之前選舉獲勝者授予的等級將從卸任的辦公室持有者（們）中撤銷，當新的獲勝者上任時。
  # 適用於城鎮選舉的城鎮等級和國家選舉的國家等級。
  revoke-previous-winner-ranks: false

  # 當決定獲勝者時執行的額外原生/Bukkit 控制台命令。
  # 佔位符：{winner} {winner_uuid} {winner_party} {party} {town} {votes} {total_votes}
  # 從控制台執行。非常適合 LuckPerms、廣播、給予物品等。
  # 留空以不執行任何命令。示例（取消註解以使用）：
  #   - "lp user {winner} parent addtemp mayor 30d"
  #   - "give {winner} minecraft:golden_helmet 1"
  commands-on-win: []

  # 當選舉結束時，對每個落選候選人執行的命令。
  # 佔位符：{loser} {loser_uuid} {loser_party} {party} {town} {votes}
  commands-on-loss: []

# ----------------------------------------------------------------------------
#  命令自訂
# ----------------------------------------------------------------------------
# 將 /election 的子命令重命名為適合你伺服器的任何名稱。
# 鍵是內部動作名稱；值是玩家在聊天中輸入的。
# 示例：將 parties: "blocs" 設置為使 /election blocs 列出政黨情況。
# 保持每個字面唯一，以便命令可以明確解析。
commands:
  run: "run"          # 註冊為候選人
  withdraw: "withdraw"  # 退出選舉
  campaign: "campaign"  # 設置你的競選訊息
  profile: "profile"    # 設置你的候選人個人資料/簡介
  party: "party"        # 加入、創建、離開或管理員重命名政黨
  parties: "parties"  # 列出當前政黨情況
  vote: "vote"          # 投票
  status: "status"      # 查看當前選舉狀態
  candidates: "candidates"  # 列出候選人
  results: "results"    # 查看上一次選舉的結果
  start: "start"        # （管理員）開始選舉
  stop: "stop"          # （管理員）提前結束投票並統計
  cancel: "cancel"      # （管理員）取消選舉，沒有獲勝者
  reload: "reload"      # （管理員）重新載入配置
  help: "help"
  nation: "nation"      # 前綴，用於定位你的國家，例如 /election nation vote

# ----------------------------------------------------------------------------
#  通知
# ----------------------------------------------------------------------------
notifications:
  # 向整個伺服器廣播選舉的開始/結束（除了城鎮）。
  broadcast-server-wide: false
  # 提醒尚未投票的投票者，在投票結束前這麼長時間。
  # 設置為 "0" 以禁用提醒。
  voting-reminder-before-end: "6h"
  # 當居民登入時，如果有進行中的選舉他們可以參與，則通知他們。
  notify-on-join: true

```

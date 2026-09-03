# 《剑与远征》AI星河创想家计划结算口径

Use this reference only for the corresponding AFK creator campaign unless the user explicitly adopts the same rules elsewhere.

## Confirmed Rules

- Group creators by 小莉创作社ID.
- Combine Bilibili and Douyin for total post count and total views, while showing each platform separately.
- The same work posted on both platforms counts as two posts; add both platforms' views.
- Reward types stack: 牛刀小试 + AI专项梯度奖 + 排名奖.
- A view count exactly equal to 500 qualifies wherever the rule says `≥500`.
- Do not enforce originality, hashtag, AI-content, duration, or content-review eligibility until the user asks.
- Do not deduct paid-traffic views until the user supplies or manually adjusts those values.

## 牛刀小试

- A creator receives ¥20 on a platform if at least one post on that platform has views `≥500`.
- Each creator account can receive this reward once per platform, so the combined maximum is ¥40.

## AI专项梯度奖

Use combined platform counts and views. Pay only the highest eligible tier:

| Posts | Views | Reward |
|---:|---:|---:|
| ≥5 | ≥10,000 | ¥100 |
| ≥5 | ≥30,000 | ¥200 |
| ≥10 | ≥50,000 | ¥300 |
| ≥10 | ≥100,000 | ¥400 |
| ≥10 | ≥200,000 | ¥800 |
| ≥15 | ≥300,000 | ¥1,000 |
| ≥15 | ≥400,000 | ¥1,200 |

- Total tier prize pool: ¥10,000.
- Allocate by each creator's first submission time, earliest first.
- Keep the theoretical highest-tier reward and actual paid reward as separate fields.
- If remaining pool balance is less than the next complete reward, do not assume partial payment; flag for confirmation unless the user already specified the treatment.

## 排名奖

- Only posts with individual views `≥500` contribute their entire view count to ranking views.
- Sum eligible Bilibili and Douyin views by creator.
- Rank 1: ¥1,000; rank 2: ¥500; rank 3: ¥300.
- Paid-traffic views are not deducted in the initial calculation.
- If ranking views tie, flag the tie for a business decision unless a tie rule has been supplied.

## Known Exception Patterns

- A link appears in the wrong platform sheet.
- A short link cannot be resolved or has expired.
- A resolved Douyin video ID is absent from the delivery dataset.
- A view cell is blank; this is not the same as zero.
- The same platform video ID or URL is submitted more than once.
- Creator names conflict under the same stable ID.

Retain these rows in an exception list with source sheet, source row, creator ID, URL/ID, issue type, and handling status.

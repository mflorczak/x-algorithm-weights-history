# X For You ranking weights: every change since August 2026

X publishes the default weights of its For You ranker in
[`home-mixer/params/param.rs`](https://github.com/xai-org/x-algorithm/blob/main/home-mixer/params/param.rs)
([xai-org/x-algorithm](https://github.com/xai-org/x-algorithm), Apache-2.0). Its README says cron scripts set
these defaults "to be the primary production values", and the first line of the file carries the time of the sync
it mirrors. X commits a new version every few days.

We read all 60 commits of that file from 13 August to 13 November 2026 and recorded every change to the weights in
its weights block, the parameters listed between `favorite_weight` and `not_dwelled_weight`: the 28 published on
13 August and the 3 added later (`react_with_video_weight`, `post_video_weight`, `grok_analyze_weight`), 53 rows
in all. Parameters outside that block are not included, even where "weight" is in their name: the out-of-network
factors (`oon_weight_factor`, `topic_oon_weight_factor`, `new_user_oon_weight_factor`), `weight_perturbation_sigma`
and the `video_carousel_*` weights.

## The file

`x-algorithm-weights.csv` has one row per change:

| Column | Meaning |
|---|---|
| `sync_utc` | The sync time in the file's first line |
| `commit` | The xai-org/x-algorithm commit that carries it |
| `weight` | The parameter name without the `rust_home_mixer_` prefix |
| `previous_value` | The value before; empty when the weight first appears |
| `new_value` | The value after; empty when the weight was removed |

The first 28 rows are the values as first published (commit `47c1bcda`, 13 August 2026; its first line says it
was synced on 12 August).

## What changed

- The like weight (`favorite_weight`) rose from 0.5 to 0.708 in three steps: 0.6 on 12 October, 0.66 on
  13 October and 0.708 on 4 November.
- The weight on sharing a post by copying its link (`share_via_copy_link_weight`) went from 20, the largest
  positive weight in the file, to 0 in the sync of 12 November.
- Not interested (`not_interested_weight`) went from −43.2 to −53.07 in three steps: 28 September, 13 October
  and 4 November.
- The reply weight stayed at 5.0.

Weights multiply predicted probabilities, not counts, as the comments in the file stress, so a reply weighted
seven times a like is not worth seven likes.

## Limits

- These are the defaults mirrored into the open-source code. X's README says its aim is for experiments running
  at a notable share of traffic, such as 10% or more, to be visible in the repository, so an account inside a
  smaller test can be ranked with other values.
- The file has 61 commits but 57 distinct sync times: the first four commits share the sync of 12 August, and two
  share the sync of 28 October.

## Explained

What each weight means and how the ranker uses it: [X algorithm 2026 guide](https://bangerkit.io/guides/x-algorithm-2026)
on Bangerkit. The same CSV is served at https://bangerkit.io/data/x-algorithm-weights.csv.

## Licence

The CSV is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use it for anything, crediting
"Bangerkit, X For You ranking weights history". The values come from xai-org/x-algorithm, Apache-2.0.

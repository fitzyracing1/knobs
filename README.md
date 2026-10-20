# knobs

> **knob** (n.): a default parameter or setting in a dependency or project that can change silently between
> versions and change how your system behaves.

You didn't change a line of your code. You bumped a version, or pulled upstream, and now the robot brakes
harder, the server trusts a different proxy, or the feed ranks likes differently. No changelog line said so.
A default moved.

## Why knobs matter

- **They're silent.** Defaults change in commits titled "update params", "cleanup" or "Open-source X
  Recommendation Algorithm". Release notes rarely list them.
- **They're behavioural.** A gain, threshold, timeout or weight is behaviour. `0.55 → 0.7` on a costmap
  inflation radius changes where a robot will drive.
- **They're inherited.** Every default you didn't set yourself is a decision someone upstream can revise.
- **They're checkable.** A default is a literal in a file. Diff the literal and you know exactly what moved,
  from what, to what, in which commit. No guessing, no LLM needed.

## Real knobs, from knoblog output

| Project | Knob | Change | Commit |
|---|---|---|---|
| X algorithm (home-mixer) | `FavoriteWeight` | 0.5 → 0.6 (Oct 13, 2026) → 0.66 (Oct 14, 2026) | [e1a0375](https://github.com/xai-org/x-algorithm/commit/e1a0375), [17c96bf](https://github.com/xai-org/x-algorithm/commit/17c96bf) |
| Nav2 | `inflation_layer/inflation_radius` | 0.55 → 0.7 (27% higher) | [nav2 demo](https://fitzyracing1.github.io/knoblog/demo/nav2/) |
| Nav2 | `collision_monitor/FootprintApproach/time_before_collision` | 2.0 → 1.2 (40% lower) | [nav2 demo](https://fitzyracing1.github.io/knoblog/demo/nav2/) |
| Nav2 | `velocity_smoother/max_accel[0]` | 2.5 → 3.0 (20% higher) | [nav2 demo](https://fitzyracing1.github.io/knoblog/demo/nav2/) |
| Nav2 | `planner_server/GridBased/tolerance` | 0.5 → 0.25, then back to 0.5 | [nav2 demo](https://fitzyracing1.github.io/knoblog/demo/nav2/) |
| PX4 | `FW_T_HRATE_FF` | 0.3 → 0.5 (67% higher) | [d84f6c3](https://github.com/PX4/PX4-Autopilot/commit/d84f6c324aec68ad3468a708036fc4cad7f298a5) |
| PX4 | `MPC_LAND_RADIUS` | 1000.f → -1.0f (sign flipped) | [1c821cf](https://github.com/PX4/PX4-Autopilot/commit/1c821cf83dcd688a185f00205700212af191e8b5) |
| ArduPilot | `AC_Loiter/OPTIONS` | 1 → 0 | [ArduPilot posts](https://github.com/fitzyracing1/knoblog/blob/main/examples/demo-output/ardupilot-posts.txt) |
| gunicorn 20.1.0 → 23.0.0 | `forwarded_allow_ips` default | `'127.0.0.1'` → `'127.0.0.1,::1'` | [guard demo PR](https://github.com/fitzyracing1/knobs-guard-demo/pull/1) |

## The toolkit

| Tool | What it does |
|---|---|
| [knoblog](https://github.com/fitzyracing1/knoblog) | Finds every changed default in a git history. Writes a site, feeds, `changes.json` and X-ready post text. `pip install knoblog` |
| [knoblog-upgrade-guard](https://github.com/fitzyracing1/knoblog-upgrade-guard) | GitHub Action that comments on dependency-bump PRs with the defaults that changed between versions |
| [knobs-watch](https://github.com/fitzyracing1/knobs-watch) | Knob changelogs for big projects (PyTorch, Kubernetes, Next.js, Home Assistant, PX4, ROS 2), refreshed on a schedule. Also hosts the multi-project X feeds and weekly email digests |
| [x-algorithm-changelog](https://fitzyracing1.github.io/x-algorithm-changelog/) | Every weight and threshold change in X's open-source recommendation algorithm |
| [repocast](https://github.com/fitzyracing1/repocast) | Turns repo changes into accurate X posts and posts them safely |

Site: <https://fitzyracing1.github.io/knobs/>

MIT licensed.

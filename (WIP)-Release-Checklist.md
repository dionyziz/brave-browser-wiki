Feel free to copy this into an issue if you want to keep track of items per-milestone.
Be super sure that <version> is replaced with the version you wish to use.

### Prerequisites

- [ ] Check https://github.com/brave/webtorrent is up to date with its latest upstream.
- [ ] Check https://github.com/brave/bittorrent-tracker is up to date with its latest upstream.
- [ ] Check https://github.com/brave/torrent-discovery is up to date with its latest upstream.
- [ ] Check Tor is up to date with its latest upstream.
- [ ] At freeze date, consult with the security team to ensure that all security issues have been included.
- [ ] At freeze date, consult with PR team (@catherinecorre) and provide heads up on release timing, screenshots, other deliverables.

### Release Notes to Staging
- [ ] Mark closed issues in github as release-notes/exclude or release-notes/include.
- [ ] Stage release notes to https://github.com/brave/brave-browser/releases/
- [ ] Stage release notes to brave.com/release/ 

### Test Staging for Updates (needs input from devops)
- [ ] Install a prior version of the app
- [ ] `BRAVE_UPDATE_HOST=https://laptop-updates-pre.brave.com open -a ./Brave.app`
- [ ] Confirm SHA in about:brave matches expectations

### Certification and Builds
- [ ] QA summary and build verification report.
- [ ] Devops starts release process. (need input from devops)

### Fastly (need input from devops)
- [ ] Log into Fastly and purge the cache

### Push To Production (need input from devops)
- [ ] `git push heroku`

### Updates Testing on Production
- [ ] Wait for confirmation that Windows live update works
- [ ] Wait for confirmation that macOS live update works
- [ ] Wait for confirmation that Linux live update works
- [ ] Update the Brave Snap Package under Ubuntu

### Download Binaries from Brave.com
- [ ] download binary from https://brave.com
- [ ] download binary from https://brave.com/download
- [ ] download binary using https://laptop-updates.brave.com/latest/winx64
- [ ] download binary using https://laptop-updates.brave.com/latest/winia32
- [ ] download binary using https://laptop-updates.brave.com/latest/osx
- [ ] download binary to test promos https://brave.com/kjo527 - kjozwiak.github.io [Production]
- [ ] download binary to test promos https://brave.com/red194 - Twitch (redPwnie) [Production]
- [ ] download binary to test promos https://brave.com/kam253 - YT (kamiljoz) [Production]
- [ ] download binary to test promos https://brave.com/bra941 - YT (braveqa1) [Production]

### Announcements
- [ ] Publish the release notes to github and brave.com/releases. (@rebron) 
- [ ] Announce release on https://community.brave.com/ (@brave-matt)
- [ ] Announce release on https://www.reddit.com/r/brave_browser/ (@brave-matt)
- [ ] Notify #general, #brave-core, #pr, #testers of the latest release with a link to the release notes

### Update Release channel wiki
- [ ] Update entries here as needed: https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule

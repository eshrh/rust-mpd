This is my fork of [rust-mpd](https://github.com/kstep/rust-mpd) which
I use in my MPD client, [inori](https://github.com/eshrh/inori).

The original program is licensed under either Apache v2 or MIT. I have
chosen the MIT license, and you can find the original
license/copyright notice [here](./LICENSE-MIT), included with the
software.

All my original code is public domain under the Unlicense.

Features I have implemented are not particularly idiomatic or well
written, but they get ~~the~~ *my* job done. New additions are:
- `listallinfo` command from an upstream
  [PR](https://github.com/kstep/rust-mpd/pull/72) by
  [paulchambaz](https://github.com/paulchambaz)
- `fn list_group_2(&mut self, terms: (String, String)) ->
  Result<Vec<(String, String)>>` which calls the "list" command for
  two terms with the group keyword, as specified in the
  [protocol](https://mpd.readthedocs.io/en/latest/protocol.html#the-music-database)
- `fn list_groups(&mut self, terms: Vec<&str>) ->
  Result<Vec<Vec<String>>>` which also calls the "list" command for an
  arbitrary number of terms. The output nested vectors contains the
  grouping structure. So, for example, a call like "title group album"
  will return
  ```
  [["album1"], ["album1", "title1"], ["album2"], ["album2 title2"]]
  ```
  and so on. This is primarily useful to obtain
  one entry for each object in the library; I use it in inori for the
  global search feature.
- resolved/suppressed all compilation warnings.

It is not possible to implement these features that I need without a
fork because the necessary Client api is not public, and the original
maintainer has been inactive for some time.

# Barnyard Readium security patch

Based on upstream Readium 3.8.0, commit f7d10d2bf5876408feae14d634416f69d1473fd8.

This Swift Package Manager fork removes marmelroy/Zip entirely (GHSA-g454-wj9r-jpg4 / CVE-2023-39135). Readium's existing ZIPFoundation reader handles both local and remote ZIP/EPUB resources. The Minizip adapter and its tests are removed because their dependency is no longer available. The ZIPFoundation tests remain unchanged. No publication, navigator, DRM or UI code is changed.

Barnyard pins this fork by immutable commit, not branch. Its app test suite covers stored/deflated archive data, ranges, malformed input, crafted archive entry names without filesystem writes, and EPUB navigation/bookmarks on iPhone and iPad. This does not certify unrelated dependencies.

Upstream notes a Minizip performance advantage for large deflated entries in LCP-protected publications. Barnyard does not enable LCP. Reassess this tradeoff before adding LCP support. Return to an upstream release only once its resolved dependency graph excludes the vulnerable package and the same regression checks pass.

Only the Swift Package Manager distribution is maintained by this patch; do not use the legacy CocoaPods specifications from this fork.

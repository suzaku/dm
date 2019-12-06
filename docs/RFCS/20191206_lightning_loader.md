# Replace Loader with Lightning

## Background

In DM, the `loader.Loader` struct implements loading data from *mydumper* output files into TiDB. Since v3.0.3, Lightning supports the TiDB backend, which enables Lightning to do the same thing.

## Proposal

We consider the TiDB backend mode of Lightning the better implementation of the two, because:

1. It has more complete parsing support that can succeed in cases `loader.Loader` would fail;
1. It has more fine-grain concurrency control, allowing users to config read and write concurrency differently.

So we propose to replace [Loader](https://github.com/pingcap/dm/blob/master/loader/loader.go) with Lightning.

# Success Criteria

- Reimplement `loader.Loader` (which is an implementation of the [Unit](https://github.com/pingcap/dm/blob/master/dm/unit/unit.go) interface) with Lightning;
- Maintain backward-compatibility of config files like `task.yaml`

# TODO list

- [ ] Refactor Lightning to make the loader path usabale as a library in DM
- [ ] Implement a new loader in DM based on Lightning

# References

- [DM 源码阅读系列文章（四）dump/load 全量同步的实现
](https://pingcap.com/blog-cn/dm-source-code-reading-4/)
- [如何使用 Lightning 导入大量数据到 TiDB/MySQL](https://docs.google.com/document/d/13U0Cud3YSThQFOzIQwt-aWjwd4M4fOKBb3JMtlQYQV4/edit#heading=h.nv8cs1ww1v84)

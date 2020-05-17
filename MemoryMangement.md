Memory Management:

- Bring pages in only when needed (demand paging of text sections)
- Keep pages brought into memory as long as possible to avoid reading from slower devices (page cache etc.)
- Under memory pressure, get rid of redundant copies of data (text pages being freed during memory pressure.
-  If required memory can not be freed as there is only one copy of it (data sections ), move the data to slower medium(swapping onto disk) and book keep the information so that they can be brought back into memory when needed.
- Use processor MMUs for isolation and privileges. These MMU components (TLBs and caches) act as a cache of page tables.
- Use optimized algorithms and data structures.

---
name: Provision a door (entry) and attach hardware
description: Create an entry and wire up its reader and relay, then identify it to confirm the wiring.
api: openapi/openpath-openapi-original.json
operations: [listAcus, createEntry, setReaderToEntry, setRelayToEntry, remoteEntryIdentify, describeEntry]
generated: '2026-07-20'
method: generated
---

# Provision a door (entry) and attach hardware

Requires a token with site/hardware write scopes (e.g. `o{orgId}-site:w`,
`o{orgId}-hw:w`). All paths are under `/orgs/{orgId}/...`.

## Steps

1. **Find the controller** — `listAcus` lists the Access Control Units (ACUs) for the
   org so you know which hardware ports are available.
2. **Create the entry** — `createEntry` creates the door/entry record under the org.
3. **Attach a reader** — `setReaderToEntry` binds a reader to the entry so credentials
   can be presented at the door.
4. **Attach a relay** — `setRelayToEntry` binds the relay (lock/strike) the entry
   actuates on a granted access.
5. **Confirm physically** — `remoteEntryIdentify` makes the entry's readers flash/buzz
   so an installer can confirm the correct door was wired.
6. **Read back** — `describeEntry` returns the final entry with its controls.

Related: `setRexToEntry`, `setContactSensorToEntry`, `setWiegandToEntry` attach the
other control types. To temporarily hold a door open/closed use `setEntryTempState`
and revert with `revertEntryTempState`.

# Frappe Framework - Custom Instance

**App:** Frappe Framework (upstream with customizations)
**Repository:** https://github.com/EricIrby/frappe.git
**Purpose:** Core framework for BLKSHP-DEV bench
**Bench:** `/Users/Eric/Development/BLKSHP/BLKSHP-DEV`

---

## Overview

This is a custom fork of the Frappe Framework maintained for the BLKSHP-DEV bench. While most functionality comes from upstream Frappe, this instance may contain BLKSHP-specific customizations.

### Upstream Information

- **Upstream Repository:** https://github.com/frappe/frappe
- **Documentation:** https://docs.frappe.io/
- **Version:** v15+
- **Purpose:** Low-code web framework for building business applications

---

## Critical Guidelines

### 1. Upstream vs Custom Code

**Upstream Code (DO NOT MODIFY):**
- Core Frappe files and functionality
- Standard DocTypes
- Framework APIs
- Build tools

**Custom Code (MAY MODIFY):**
- BLKSHP-specific patches
- Custom integrations
- Site-specific configurations
- Any files in `custom/` directories

### 2. Update Strategy

**Before Pulling Upstream:**
```bash
# Check for local modifications
git -C /Users/Eric/Development/BLKSHP/BLKSHP-DEV/apps/frappe status

# Check what's different from upstream
git -C /Users/Eric/Development/BLKSHP/BLKSHP-DEV/apps/frappe diff upstream/main

# Pull carefully
git -C /Users/Eric/Development/BLKSHP/BLKSHP-DEV/apps/frappe pull upstream main
```

**After Updating:**
- Test all BLKSHP apps: `./env/bin/bench --site blkshp.local migrate`
- Run tests: `./env/bin/bench run-tests --app blkshp_os`
- Check for breaking changes in Frappe release notes

---

## Working with Frappe

### Development Commands

```bash
# Always use bench venv
./env/bin/bench --help

# Clear cache (fixes many issues)
./env/bin/bench --site blkshp.local clear-cache

# Rebuild assets
./env/bin/bench build

# Watch for changes (development)
./env/bin/bench watch

# Console (Python REPL with Frappe context)
./env/bin/bench --site blkshp.local console
```

### Common Frappe Patterns

**Get a document:**
```python
import frappe
doc = frappe.get_doc("DocType Name", "document-name")
```

**Query database:**
```python
results = frappe.get_all(
    "DocType Name",
    filters={"field": "value"},
    fields=["name", "field1", "field2"]
)
```

**Create document:**
```python
doc = frappe.get_doc({
    "doctype": "DocType Name",
    "field": "value"
})
doc.insert()
```

---

## Customization Tracking

### Custom Patches

Document any custom patches or modifications here:

**Format:**
```
Date: YYYY-MM-DD
File: path/to/file.py
Reason: Why this customization was needed
Issue: BLK-XXX (if applicable)
```

### Integration Points

**BLKSHP OS Integration:**
- JWT Authentication hooks
- Custom permissions system
- Feature flag infrastructure

---

## Troubleshooting

### Frappe Won't Start

```bash
# Check logs
tail -f /Users/Eric/Development/BLKSHP/BLKSHP-DEV/logs/bench-start.log

# Check if venv is activated
which python  # Should be ./env/bin/python

# Reinstall app
./env/bin/bench --site blkshp.local reinstall
```

### Migration Issues

```bash
# Force migrate
./env/bin/bench --site blkshp.local migrate --force

# Check migration logs
tail -f /Users/Eric/Development/BLKSHP/BLKSHP-DEV/logs/bench-start.log
```

### Build Errors

```bash
# Clear cache and rebuild
./env/bin/bench --site blkshp.local clear-cache
./env/bin/bench build --force

# If node_modules are corrupted
cd apps/frappe
rm -rf node_modules
npm install
cd ../..
./env/bin/bench build
```

---

## Important Notes

### For AI Assistants (Claude)

1. **Don't modify upstream code** unless absolutely necessary
2. **Document all customizations** in this file
3. **Test after Frappe updates** to ensure BLKSHP apps still work
4. **Use Frappe APIs** instead of direct database access
5. **Follow Frappe conventions** for consistency
6. **Check Frappe docs** before asking questions: https://docs.frappe.io/

### For Developers

1. **Stay close to upstream** - minimize customizations
2. **Contribute upstream** when possible (bug fixes, features)
3. **Test thoroughly** after framework updates
4. **Monitor breaking changes** in Frappe release notes
5. **Use Frappe CLI** for all framework operations

---

## Resources

- **Frappe Documentation:** https://docs.frappe.io/
- **Frappe GitHub:** https://github.com/frappe/frappe
- **Frappe Discuss:** https://discuss.frappe.io/
- **Bench Documentation:** https://frappeframework.com/docs/user/en/bench

---

## Related Files

- **Bench-level context:** `/Users/Eric/Development/BLKSHP/BLKSHP-DEV/CLAUDE.md`
- **Cursor rules:** `/Users/Eric/Development/BLKSHP/BLKSHP-DEV/.cursor/rules`
- **BLKSHP OS context:** `/Users/Eric/Development/BLKSHP/BLKSHP-DEV/apps/blkshp_os/CLAUDE.md`

---

**End of Frappe Context Document**

*This document focuses on Frappe Framework customizations and integration with BLKSHP-DEV bench. For Frappe core functionality, refer to official Frappe documentation.*

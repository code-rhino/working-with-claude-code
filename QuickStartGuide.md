# T-Commands Quick Reference Guide

*Original framework by Sabrina Ramonov | Enhanced by Tariq Hook*

## 🚀 Development Workflow Commands

### **TNEW** - Initialize Development Session
```
Understand all best practices from CLAUDE.md guide
Focus on: architecture patterns, external integrations, async design patterns
```

### **TPLAN** - Analyze & Plan Implementation  
```
Analyze existing codebase for consistency:
✓ Architecture and module organization compliance
✓ External integration patterns if applicable
✓ Minimal changes approach
✓ Code reuse opportunities
✓ Security and performance implications
✓ Feature flag and deployment considerations
```

---

## 🛡️ Safe Implementation Workflow

### **TREF** - Prepare Safe Implementation *(optional for risky changes)*
```
Create safety checkpoint before major changes:
1. git add . && git commit -m "checkpoint: save work before refactoring"
2. git checkout -b $(git branch --show-current)-working
3. Proceed with implementation on working branch

USE FOR: Multiple files, signature changes, core logic, external integrations
SKIP FOR: Bug fixes, new methods, docs, config changes
```

### **TCODE** - Implement with Quality Gates *(always)*
```
Implement plan with full validation:
✓ Run all tests
✓ [formatting tool] (e.g., prettier, black, spotless)
✓ [build/compile] passes without warnings
✓ Test with appropriate [environment/profile]
✓ Feature flag validation (enabled/disabled states)
```

### **TMERGE** - Complete Safe Implementation *(if TREF was used)*
```
Merge working branch back safely:
1. Ensure all tests pass on working branch
2. git checkout <original-branch>
3. git merge <original-branch>-working
4. git branch -d <original-branch>-working
5. git push origin <original-branch>

RECOVERY: git checkout <original-branch> && git branch -D <branch>-working
```

---

## 🔍 Quality Assurance Commands

### **TCHECK** - Comprehensive Code Review
```
SKEPTICAL senior engineer analysis for MAJOR changes:
✓ Writing Functions/Methods Best Practices checklist
✓ Writing Tests Best Practices checklist  
✓ Implementation Best Practices checklist
✓ Architecture and module organization compliance
✓ External integration impact assessment
✓ Performance patterns and feature flag compliance
```

### **TCHECKF** - Function/Method Review
```
Focused analysis for MAJOR functions/methods:
✓ Writing Functions/Methods Best Practices checklist only
```

### **TCHECKT** - Test Review
```
Focused analysis for MAJOR tests:
✓ Writing Tests Best Practices checklist only
```

---

## 🎯 Specialized Commands

### **TUX** - User Experience Testing
```
Human UX tester perspective for implemented features:
📋 Comprehensive test scenarios (priority-ordered)
🎯 Focus areas: key user workflows, external integrations, platform considerations
```

### **TGIT** - Professional Git Commit
```
Stage, commit, and push with standards:
✓ Conventional Commits format
✓ Structured commit message
✓ No Claude/Anthropic references
✓ Proper semantic versioning correlation
```

---

## 📋 Safe Implementation Decision Tree

```
Starting new work?               → TNEW
Planning implementation?         → TPLAN  

Risky/complex changes?           → TREF → TCODE → TMERGE
Simple changes?                  → TCODE only

Code review needed?             → TCHECK / TCHECKF / TCHECKT
Testing scenarios?              → TUX
Ready to commit?                → TGIT
```

---

## 🛡️ Implementation Safety Levels

### **Level 1: Basic Implementation**
```
TPLAN → TCODE → TGIT
For: New features, bug fixes, simple additions
```

### **Level 2: Safe Implementation** 
```
TPLAN → TREF → TCODE → TMERGE → TGIT
For: Refactoring, signature changes, core business logic
```

### **Level 3: Mission Critical Implementation**
```
TPLAN → TREF → TCODE → TCHECK → TMERGE → TUX → TGIT
For: Core features, external integrations, production-critical changes
```

---

## ⚠️ Implementation Guidelines

### **When to Use TREF (Safety Checkpoint)**
- ✅ **DO USE**: Multiple files, function/method signatures, core business logic, external integrations, async patterns
- ❌ **SKIP**: Bug fixes, adding new functions/methods, documentation, configuration changes

### **TCODE is Always Required**
- Every implementation must pass quality gates
- Format, compile, test, and validate before proceeding

### **TMERGE Only After TREF**
- If you used TREF, you MUST use TMERGE to complete the safe workflow
- Never leave working branches hanging

---

## 🔧 Environment Context

- **Environments**: [development, staging, production, testing]
- **Architecture**: [your module/package organization]
- **External Integrations**: [authentication, APIs, services]
- **Technology Stack**: [your specific tools and frameworks]
- **Database**: [your database and migration system]

---

## 💡 Pro Tips

- **Always start with TNEW** to load the right context
- **TPLAN before coding** saves time and prevents architectural mistakes  
- **Use TREF for anything that makes you nervous** - better safe than sorry
- **TCHECK commands skip minor changes** - focus on architectural impact
- **The three safety levels** help choose the right workflow for the risk level
- **Adapt commands to your tech stack** - replace [placeholders] with your tools

---

## 🛠️ Customization Guide

To adapt this guide for your project:

1. **Replace [placeholders]** with your specific tools and commands
2. **Update Environment Context** with your actual architecture
3. **Modify TUX focus areas** for your domain and user workflows
4. **Customize TCODE** quality gates for your build system
5. **Add project-specific safety considerations** to TREF guidelines

This command system works with any technology stack while maintaining professional development workflow standards.
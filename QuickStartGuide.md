# T-Commands Quick Start

*Development workflow commands for efficient Claude conversations*

## Example: Adding a User Authentication Feature

Here's how a real conversation with Claude might look using T-commands:

**You:** I need to add user authentication to my React app with login/logout and protected routes. tnew

**Claude:** I'll help you implement user authentication. Starting with TNEW to understand your architecture...

*[Claude examines your codebase and identifies React setup, routing library, existing patterns]*

**You:** tplan

**Claude:** Based on your React app with React Router, here's my implementation plan:

1. Create AuthContext for state management
2. Add login/logout components using existing UI patterns
3. Implement ProtectedRoute wrapper component
4. Add authentication hooks
5. Update routing configuration

This follows your existing patterns: Context API for state, component composition, and your current styling approach.

**You:** Looks good, but make it work with our existing API endpoints. tcode

**Claude:** Implementing authentication system...

*[Claude implements the complete authentication system, runs tests, formats code]*

✓ All tests passing
✓ Code formatted with Prettier
✓ TypeScript compilation successful
✓ Authentication flow working with your existing `/api/auth` endpoints

**You:** tcheck

**Claude:** Reviewing implementation as a skeptical senior engineer...

✓ **Functions:** Clean, testable, single responsibility
✓ **Tests:** Comprehensive coverage for auth flows and edge cases
✓ **Architecture:** Follows your existing Context pattern consistently
✓ **Security:** Proper token handling, no sensitive data in localStorage
✓ **Integration:** Seamlessly works with existing API structure

The implementation is solid and follows your established patterns.

**You:** Perfect! tgit

**Claude:** 
```bash
git add .
git commit -m "feat: add user authentication with login/logout and protected routes"
git push origin main
```

Authentication feature successfully implemented and committed!

---

## Core T-Commands

### **TNEW** - Start Smart
```
"tnew" = Load all project context and best practices
```
**Example prompt:** *"I need to add a shopping cart feature. tnew"*

### **TPLAN** - Plan Implementation
```
"tplan" = Analyze codebase and create implementation plan
```
**Example prompt:** *"tplan"* *(after describing your feature)*

### **TCODE** - Implement & Validate
```
"tcode" = Build the feature with quality gates
```
**Example prompt:** *"The plan looks good. tcode"*

### **TCHECK** - Code Review
```
"tcheck" = Senior engineer review of your implementation
```
**Example prompt:** *"tcheck"* *(after implementation)*

### **TGIT** - Professional Commit
```
"tgit" = Commit with proper conventional commit format
```
**Example prompt:** *"Ready to commit. tgit"*

---

## Safety Commands (For Complex Changes)

### **TREF** - Create Safety Checkpoint
```
"tref" = Create git checkpoint before risky changes
```
**Use when:** Refactoring multiple files, changing APIs, core business logic

**Example prompt:** *"I need to refactor the entire payment system. tref"*

### **TMERGE** - Complete Safe Implementation
```
"tmerge" = Merge working branch back safely
```
**Use after:** TREF when implementation is complete

**Example prompt:** *"Tests are passing, ready to finalize. tmerge"*

---

## Specialized Commands

### **TUX** - User Testing Scenarios
```
"tux" = Generate comprehensive test scenarios
```
**Example prompt:** *"tux"* *(after implementing a user-facing feature)*

### **TCHECKF/TCHECKT** - Focused Reviews
```
"tcheckf" = Review specific functions only
"tcheckt" = Review specific tests only
```
**Example prompt:** *"tcheckf"* *(for complex algorithm review)*

---

## Quick Decision Guide

```
Simple feature/bug fix:     → TNEW → TPLAN → TCODE → TGIT
Complex feature:            → TNEW → TPLAN → TCODE → TCHECK → TGIT  
Risky refactoring:          → TNEW → TPLAN → TREF → TCODE → TMERGE → TGIT
```

---

## Pro Tips

1. **Always start with TNEW** - Claude loads your project context
2. **TPLAN saves time** - Get the approach right before coding
3. **Use TREF when nervous** - Better safe than sorry
4. **One T-command per message** - Let Claude complete each step
5. **Combine naturally:** *"Looks good, tcode"* or *"Done with that, tgit"*

The T-commands turn Claude into your pair programming partner with built-in best practices and safety nets.
# 🤝 Contributing to Kotlin Multiplatform Learning Roadmap

Chúng tôi rất hoan nghênh mọi đóng góp để làm cho lộ trình học này tốt hơn! 

## 🌟 Cách Bạn Có Thể Đóng Góp

### 📝 Content Contributions
- **Cập nhật tài nguyên học tập** mới và hữu ích
- **Bổ sung examples và code samples**
- **Cải thiện documentation** và fix typos
- **Dịch nội dung** sang các ngôn ngữ khác
- **Thêm exercises và challenges** cho từng tuần

### 🐛 Bug Reports
- **Report broken links** trong RESOURCES.md
- **Fix outdated information** về versions, APIs
- **Improve setup instructions** trong SETUP-GUIDE.md

### 💡 Feature Requests
- **Suggest new learning paths** cho advanced topics
- **Propose new project ideas** cho practice
- **Request additional platforms** (Desktop, Web)

## 📋 Contribution Guidelines

### 🚀 Getting Started

1. **Fork** repository này
2. **Clone** fork về máy local:
   ```bash
   git clone https://github.com/[your-username]/kotlin-multiplatform-learning-roadmap.git
   cd kotlin-multiplatform-learning-roadmap
   ```
3. **Create branch** mới cho feature/fix:
   ```bash
   git checkout -b feature/your-feature-name
   # hoặc
   git checkout -b fix/your-bug-fix
   ```

### ✍️ Making Changes

#### 📚 Content Standards
- **Tiếng Việt:** Sử dụng tiếng Việt chính xác, tránh Tiếng Việt Telex
- **Code Examples:** Sử dụng syntax highlighting với language tags
- **Links:** Kiểm tra tất cả links hoạt động
- **Formatting:** Follow Markdown best practices
- **Emojis:** Sử dụng emojis một cách consistent với style hiện tại

#### 🏗️ File Structure
```
├── README.md               # Main overview
├── ROADMAP.md             # 8-week detailed roadmap  
├── CHECKLIST.md           # Step-by-step checklist
├── RESOURCES.md           # Learning resources & links
├── SETUP-GUIDE.md         # Environment setup guide
├── PROJECT-STRUCTURE.md   # Project architecture guide
└── CONTRIBUTING.md        # This file
```

#### 📝 Content Guidelines

**Khi thêm resources mới:**
- Verify links hoạt động
- Provide brief description
- Categorize appropriately
- Check for duplicates

**Khi update roadmap:**
- Maintain time estimates
- Keep learning objectives clear
- Include practical exercises
- Balance theory và hands-on

**Code examples:**
```kotlin
// ✅ Good: Clear, commented, working example
@Composable
fun UserItem(
    user: User,
    onClick: () -> Unit
) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .clickable { onClick() }
    ) {
        Text(text = user.name)
    }
}

// ❌ Avoid: Incomplete, unclear examples
fun someFunction() {
    // TODO: implement
}
```

### 🔍 Code Review Process

1. **Self-review** changes trước khi submit
2. **Test all links** và examples
3. **Check spelling** và grammar
4. **Ensure consistency** với existing style

### 📤 Submitting Changes

1. **Commit** changes với clear messages:
   ```bash
   git add .
   git commit -m "feat: add advanced testing section to roadmap"
   # hoặc
   git commit -m "fix: update broken links in resources"
   # hoặc
   git commit -m "docs: improve setup instructions for Windows"
   ```

2. **Push** changes lên fork:
   ```bash
   git push origin feature/your-feature-name
   ```

3. **Create Pull Request** với:
   - **Clear title** mô tả change
   - **Detailed description** về what và why
   - **Screenshots** nếu có UI changes
   - **Testing notes** nếu applicable

### 📋 Pull Request Template

```markdown
## 📝 Description
Brief description of changes made.

## 🎯 Type of Change
- [ ] Bug fix
- [ ] New feature  
- [ ] Documentation update
- [ ] Resource addition/update
- [ ] Translation

## ✅ Checklist
- [ ] Self-reviewed code/content
- [ ] Tested all links
- [ ] Followed style guidelines
- [ ] Updated relevant documentation

## 📸 Screenshots (if applicable)
Add screenshots for UI changes.

## 🧪 Testing Notes
How to test these changes.
```

## 🎯 Specific Contribution Areas

### 🔗 Resources & Links
**Cần cập nhật thường xuyên:**
- New KMP releases và features
- Updated course links và pricing
- New blog posts và tutorials
- Community resources

**Format:**
```markdown
- **[Resource Name](https://link.com)** - Brief description
```

### 📚 Learning Content
**Types of content contributions:**
- Beginner-friendly explanations
- Advanced topics và patterns
- Real-world examples
- Common pitfalls và solutions

### 🛠️ Tools & Setup
**Helping improve:**
- Platform-specific setup instructions
- Troubleshooting common issues
- Tool recommendations
- Environment optimizations

### 🌍 Translations
**Current supported languages:**
- Vietnamese (primary)
- English (secondary)

**To add new language:**
1. Create new directory: `translations/[language-code]/`
2. Translate core files
3. Update main README với language links

## 📞 Community & Support

### 💬 Communication Channels
- **GitHub Issues:** Bug reports và feature requests
- **GitHub Discussions:** Questions và ideas
- **Pull Requests:** Code/content contributions

### 🤔 Questions?
- Check existing **Issues** và **Discussions** first
- Create new **Discussion** for questions
- Create **Issue** for bugs/feature requests

### 🏷️ Labels
We use these labels để categorize contributions:
- `enhancement`: New features/improvements
- `bug`: Bug fixes
- `documentation`: Documentation updates
- `good first issue`: Good for newcomers
- `help wanted`: Extra attention needed
- `translation`: Translation work

## 🏆 Recognition

### 📈 Contributor Stats
Regular contributors sẽ được:
- Listed trong README contributors section
- Mentioned trong release notes
- Invited to join maintainer team (for significant contributions)

### 🎖️ Types of Contributors
- **Content Creators:** Add/improve learning materials
- **Technical Reviewers:** Review code examples và architecture
- **Community Managers:** Help với issues và discussions
- **Translators:** Translate content to other languages

## 📜 Code of Conduct

### 🤝 Our Pledge
Chúng tôi cam kết tạo một môi trường:
- **Welcoming** và inclusive
- **Respectful** của diverse viewpoints
- **Focused** on learning và improvement
- **Collaborative** và supportive

### 🚫 Unacceptable Behavior
- Harassment hoặc discriminatory language
- Spam hoặc self-promotion
- Off-topic discussions
- Disrespectful comments

### 📢 Reporting
Report issues to maintainers via GitHub Issues hoặc email.

---

**🙏 Thank you** for considering contributing to this project! Your efforts help thousands of developers learn KMP effectively.

**🚀 Ready to contribute?** 
1. Fork repository
2. Pick an issue from [Issues](https://github.com/[username]/kotlin-multiplatform-learning-roadmap/issues)
3. Start coding/writing!

**📧 Questions?** Feel free to reach out via GitHub Discussions.
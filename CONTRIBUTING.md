---
layout: page
title: Contributing Guide
permalink: /contributing/
description: Guidelines for contributing to the Engineering Practices Handbook. Learn how to add content, report issues, and help improve our engineering standards.
category: Community
tags: [contributing, community, guidelines, handbook]
last_updated: 2024-11-06
---

# Contributing to the Engineering Practices Handbook

Welcome! This handbook is a collaborative effort that benefits from the knowledge and experience of all team members. Your contributions help create a comprehensive resource that strengthens our engineering practices.

## 🎯 Contribution Philosophy

This handbook succeeds when it:
- **Reflects Real Experience**: Content should be based on actual practice, not theoretical ideals
- **Stays Current**: Regular updates ensure practices remain relevant and effective
- **Serves All Levels**: Content should be accessible to beginners while valuable to experts
- **Maintains Quality**: High-quality, well-structured content helps everyone learn effectively

## 📝 Types of Contributions

### 🆕 New Content
- **Practice Guides**: Comprehensive guides for specific engineering practices
- **Templates**: Reusable templates for common engineering activities
- **Checklists**: Quality assurance and process checklists
- **Decision Matrices**: Tools for making informed technical decisions
- **Case Studies**: Real examples demonstrating best practices

### 🔧 Content Improvements
- **Updates**: Refresh outdated information with current best practices
- **Clarifications**: Improve explanations and add missing context
- **Examples**: Add practical examples and code samples
- **Links**: Update broken links and add relevant external resources
- **Organization**: Improve content structure and navigation

### 🐛 Issues & Corrections
- **Error Reports**: Identify and fix inaccuracies in existing content
- **Broken Links**: Report and fix broken internal/external links
- **Outdated Practices**: Flag content that no longer reflects current best practices
- **Missing Content**: Identify gaps in handbook coverage

## 🚀 Getting Started

### 1. Identify Your Contribution
- Browse existing content to understand current coverage
- Check [GitHub Issues](https://github.com/your-org/Engineering-Practices-SE/issues) for requested content
- Review [`tags-index.md`](tags-index.md) to see content organization
- Consider areas where your expertise can add value

### 2. Plan Your Contribution
- **Small Changes**: Typos, link fixes, minor updates - contribute directly
- **Medium Changes**: New sections, significant updates - create an issue first
- **Large Changes**: New practice areas, restructuring - discuss with team leads

### 3. Follow Our Standards
- Review this contributing guide completely
- Use the templates provided in [`assets/templates/`](assets/templates/)
- Follow our documentation standards (detailed below)
- Ensure consistency with existing content style

## 📏 Documentation Standards

### Content Structure
```markdown
# Title (H1 - Main Topic)
Brief introduction paragraph explaining the purpose and scope.

## Overview (H2 - Section Headers)
Section content with practical guidance.

### Subsection (H3 - Detailed Topics)
Detailed information and examples.

#### Implementation Details (H4 - Specific Details)
Specific implementation guidance when needed.
```

### Writing Style
- **Clear and Concise**: Use plain English, avoid unnecessary jargon
- **Action-Oriented**: Focus on what to do, not just what to know
- **Practical**: Include examples, templates, and real-world scenarios
- **Scannable**: Use headings, bullet points, and formatting for readability

### Markdown Standards

#### Links and References
```markdown
# Internal Links (REQUIRED FORMAT)
[`filename.ext`](relative/path/filename.ext) - for file references
[`function.method()`](relative/path/file.ext:line) - for code references
[Section Name](relative/path/README.md#section) - for section links

# External Links
[Resource Name](https://external-url.com) - descriptive text
```

#### Code Examples
```markdown
# Inline code
Use `backticks` for inline code, function names, and file paths.

# Code blocks
```language
// Always specify language for syntax highlighting
function example() {
    return "formatted code";
}
```
```

#### Lists and Tables
```markdown
# Unordered Lists
- Primary points use hyphens
  - Sub-items use proper indentation
  - Keep consistent formatting

# Ordered Lists
1. Step-by-step processes
2. Sequential procedures
3. Numbered requirements

# Tables
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Data     | Data     | Data     |
```

### Content Organization

#### File Naming
- Use lowercase with hyphens: `best-practices.md`
- Be descriptive: `api-design-guidelines.md`
- Include README.md in each directory for navigation

#### Directory Structure
- Follow existing structure in [`NAVIGATION.md`](NAVIGATION.md)
- Place content in appropriate practice area directories
- Use subdirectories for complex topics

#### Tags and Metadata
Include relevant tags at the end of documents:
```markdown
---
**Tags**: #development #testing #automation #intermediate
**Roles**: Developer, QA Engineer
**Last Updated**: November 2024
**Related**: [`testing-strategies.md`](../testing-strategies/), [`code-review-process.md`](../../01-development-practices/code-review-process/)
```

## 🔄 Review Process

### Pull Request Requirements
1. **Clear Description**: Explain what you're adding/changing and why
2. **Scope**: Keep PRs focused - one topic per PR when possible
3. **Templates**: Use our [PR template](.github/PULL_REQUEST_TEMPLATE.md)
4. **Testing**: For templates/checklists, test them in real scenarios
5. **Links**: Verify all internal and external links work

### Review Criteria
Reviewers will evaluate:
- **Accuracy**: Content is technically correct and current
- **Completeness**: Sufficient detail for intended audience
- **Clarity**: Writing is clear and well-organized
- **Consistency**: Style matches existing handbook content
- **Value**: Content provides practical benefit to team members

### Review Timeline
- **Small Changes**: 1-2 business days
- **Medium Changes**: 3-5 business days
- **Large Changes**: 1-2 weeks (may require team discussion)

## 📋 Content Templates

### Practice Guide Template
Use [`assets/templates/practice-guide-template.md`](assets/templates/practice-guide-template.md) for:
- Comprehensive practice documentation
- Step-by-step implementation guides
- Best practice compilations

### Checklist Template
Use [`assets/templates/checklist-template.md`](assets/templates/checklist-template.md) for:
- Quality assurance checklists
- Process validation lists
- Review criteria

### Decision Matrix Template
Use [`assets/templates/decision-matrix-template.md`](assets/templates/decision-matrix-template.md) for:
- Technology selection criteria
- Process improvement decisions
- Tool evaluation matrices

## 🏷️ Tagging Guidelines

### Tag Categories
- **Technology**: `#javascript`, `#python`, `#docker`, `#kubernetes`
- **Role**: `#developer`, `#architect`, `#devops`, `#qa`
- **Type**: `#guide`, `#template`, `#checklist`, `#example`
- **Complexity**: `#beginner`, `#intermediate`, `#advanced`
- **Practice**: `#testing`, `#security`, `#architecture`, `#process`

### Tagging Rules
1. Use 3-7 relevant tags per document
2. Include at least one role and complexity tag
3. Use consistent tag formats (lowercase, hyphens for multi-word)
4. Update [`tags-index.md`](tags-index.md) when adding new tags

## ✅ Quality Checklist

Before submitting your contribution:

### Content Quality
- [ ] Information is accurate and up-to-date
- [ ] Examples are practical and tested
- [ ] Writing is clear and well-organized
- [ ] Content serves the intended audience level
- [ ] Links to related practices are included

### Technical Standards
- [ ] Markdown formatting is correct
- [ ] All links work (internal and external)
- [ ] Code examples include syntax highlighting
- [ ] Images/diagrams are properly referenced
- [ ] File is saved in appropriate directory

### Handbook Integration
- [ ] Content follows established patterns
- [ ] Tags are appropriate and consistent
- [ ] Navigation links are updated if needed
- [ ] Related documents reference new content
- [ ] [`tags-index.md`](tags-index.md) is updated if needed

## 🆘 Getting Help

### Questions About Contributing
- Create a [GitHub Issue](https://github.com/your-org/Engineering-Practices-SE/issues) with the "question" label
- Reach out to handbook maintainers
- Check [`NAVIGATION.md`](NAVIGATION.md) for existing content organization

### Technical Support
- For Markdown formatting: [GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)
- For Git/GitHub: [GitHub Documentation](https://docs.github.com/)
- For content ideas: Review [`practice-dependencies.md`](practice-dependencies.md) for gaps

### Content Inspiration
- Review external resources in [`09-reference-materials/external-resources/`](09-reference-materials/external-resources/)
- Check industry best practices and emerging trends
- Consider team-specific needs and challenges
- Look at successful implementations from other organizations

## 🎉 Recognition

Contributors to the handbook are recognized through:
- **Commit History**: GitHub tracks all contributions
- **Release Notes**: Significant contributions highlighted in updates
- **Team Recognition**: Contributions mentioned in team communications
- **Expertise Building**: Contributing builds your reputation as a subject matter expert

## 📞 Contact

**Handbook Maintainers**: Engineering Leadership Team  
**Questions**: Create a GitHub Issue or reach out directly  
**Suggestions**: Use our [suggestion template](.github/ISSUE_TEMPLATE.md)

---

**Thank you for contributing to our engineering excellence!** 🚀

Your contributions make this handbook a valuable resource for the entire engineering team. Every improvement, no matter how small, helps us build better software and stronger practices.
# Multi-Platform Publisher (다중 플랫폼 퍼블리셔)

A flexible automation framework for publishing content across multiple social media platforms with multi-language support and AI integration.
(다국어 지원 및 AI 통합을 통해 여러 소셜 미디어 플랫폼에 콘텐츠를 게시하는 유연한 자동화 프레임워크)

## Features (기능)

### 🚀 Core Capabilities (핵심 기능)
- **Multi-Platform Support (다중 플랫폼 지원)**: Currently supports Threads, easily extensible to other platforms
- **YAML Configuration (YAML 구성)**: Simple, human-readable workflow definitions
- **Multi-Language Translation (다국어 번역)**: Automatic content localization for global audiences
- **AI Integration (AI 통합)**: Gemini AI integration for enhanced automation capabilities
- **Schema Validation (스키마 검증)**: JSON schema validation ensures configuration integrity

### 🔧 Technical Features (기술적 기능)
- **Modular Architecture (모듈식 아키텍처)**: Easy to extend and customize
- **Error Handling (오류 처리)**: Comprehensive error handling and logging
- **Security First (보안 우선)**: Environment variable-based token management
- **Developer Friendly (개발자 친화적)**: Clear documentation and examples

## Quick Start (빠른 시작)

### Prerequisites (전제 조건)
```bash
pip install -r requirements.txt
```

### Basic Usage (기본 사용법)
1. **Configure your workflow (워크플로 구성)**:
```yaml
# threads_automation_config.yaml
workflows:
  - name: daily_posts
    accounts:
      - my_english_account
      - my_japanese_account
    content_source: content.txt
    translation_source_language: ko
    language_map:
      my_english_account: en
      my_japanese_account: ja
```

2. **Create content file (콘텐츠 파일 생성)**:
```bash
echo "안녕하세요! 오늘의 소식을 전해드립니다." > content.txt
```

3. **Run the automation (자동화 실행)**:
```bash
python threads_automator.py
```

## Configuration Guide (구성 가이드)

### Workflow Configuration (워크플로 구성)
The framework uses YAML configuration files to define automation workflows:
(프레임워크는 YAML 구성 파일을 사용하여 자동화 워크플로를 정의합니다)

```yaml
workflows:
  - name: "workflow_name"              # Unique workflow identifier
    accounts: ["account1", "account2"] # Target platform accounts
    content_source: "content.txt"      # Source content file path
    translation_source_language: "ko"  # Original content language
    language_map:                      # Account-to-language mapping
      account1: "en"                   # English for account1
      account2: "ja"                   # Japanese for account2
```

### Supported Languages (지원 언어)
- `ko` - Korean (한국어)
- `en` - English (영어)
- `ja` - Japanese (일본어)
- `id` - Indonesian (인도네시아어)
- More languages can be added easily (더 많은 언어를 쉽게 추가할 수 있습니다)

### AI Integration Setup (AI 통합 설정)
Configure Gemini AI integration in `.gemini/settings.json`:
(`.gemini/settings.json`에서 Gemini AI 통합을 구성합니다)

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "GITHUB_PERSONAL_ACCESS_TOKEN", "ghcr.io/github/github-mcp-server"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

## Architecture (아키텍처)

### System Overview (시스템 개요)
```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   YAML Config   │───▶│  Main Processor  │───▶│  Platform APIs  │
│   (workflows)   │    │  (automator.py)  │    │  (Threads, etc) │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │ Translation API  │
                       │ (multi-language) │
                       └──────────────────┘
```

### Component Structure (구성 요소 구조)
- **`threads_automator.py`**: Core automation engine (핵심 자동화 엔진)
- **`threads_automation_config.yaml`**: Workflow definitions (워크플로 정의)
- **`.schema/threads_automation_schema.json`**: Configuration validation (구성 검증)
- **`.gemini/settings.json`**: AI integration settings (AI 통합 설정)
- **`requirements.txt`**: Python dependencies (Python 의존성)

## Platform Integration (플랫폼 통합)

### Currently Supported (현재 지원)
- **Threads**: Via Instagram Graph API (Instagram Graph API를 통해)

### Adding New Platforms (새 플랫폼 추가)
To add support for new platforms, implement the posting function:
(새 플랫폼 지원을 추가하려면 게시 함수를 구현하세요)

```python
def post_to_new_platform(account_id, content):
    """
    Implement platform-specific posting logic here
    (여기에 플랫폼별 게시 로직을 구현하세요)
    """
    # Your platform API integration
    pass
```

## Development (개발)

### Setting Up Development Environment (개발 환경 설정)
```bash
# Clone the repository (저장소 복제)
git clone https://github.com/zdpk-automation/multi-platform-publisher.git
cd multi-platform-publisher

# Install dependencies (의존성 설치)
pip install -r requirements.txt

# Set up environment variables (환경 변수 설정)
export GITHUB_PERSONAL_ACCESS_TOKEN="your_token_here"
```

### Running Tests (테스트 실행)
```bash
# Validate configuration schema (구성 스키마 검증)
python -c "import yaml, json, jsonschema; 
config = yaml.safe_load(open('automation/social/threads_automation_config.yaml')); 
schema = json.load(open('automation/social/.schema/threads_automation_schema.json')); 
jsonschema.validate(config, schema); 
print('Configuration is valid!')"
```

### Contributing (기여하기)
1. Fork the repository (저장소 포크)
2. Create a feature branch (기능 브랜치 생성)
3. Follow the PR guidelines in `automation/social/PR_GUIDELINES.md`
4. Submit a pull request (풀 리퀘스트 제출)

## Roadmap (로드맵)

### Phase 1: Core Framework (1단계: 핵심 프레임워크) ✅
- [x] YAML-based configuration system
- [x] Multi-language translation framework
- [x] Threads API integration structure
- [x] JSON schema validation

### Phase 2: Production Ready (2단계: 프로덕션 준비)
- [ ] Real translation API integration (Google Translate, DeepL)
- [ ] Actual Threads API implementation
- [ ] Comprehensive error handling and retry logic
- [ ] Logging and monitoring system

### Phase 3: Advanced Features (3단계: 고급 기능)
- [ ] Additional platform support (Twitter, LinkedIn, Facebook)
- [ ] Scheduling system with cron-like functionality
- [ ] Content generation AI integration
- [ ] Analytics and reporting dashboard

### Phase 4: Enterprise Features (4단계: 엔터프라이즈 기능)
- [ ] Database integration for workflow history
- [ ] Queue system for high-volume processing
- [ ] Microservices architecture
- [ ] Web-based management interface

## License (라이선스)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
(이 프로젝트는 MIT 라이선스 하에 라이선스가 부여됩니다 - 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요)

## Support (지원)

- 📧 Issues: [GitHub Issues](https://github.com/zdpk-automation/multi-platform-publisher/issues)
- 📖 Documentation: [Wiki](https://github.com/zdpk-automation/multi-platform-publisher/wiki)
- 💬 Discussions: [GitHub Discussions](https://github.com/zdpk-automation/multi-platform-publisher/discussions)

---

**Built with ❤️ by the zdpk-automation team**
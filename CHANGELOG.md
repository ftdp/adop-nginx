# Changelog

All notable changes to this project will be documented in this file.
This project adheres to [Semantic Versioning](http://semver.org/).

## 0.3.3 - 2017-10-02
### Added
- SSL/HTTP support 
- LDAPS support
- CUSTOM_CONF and CUSTOM_HTML environment variables implemented to allow disabling data copy from container to the volumes on container startup (i.e. when yuo want to modify HTML or change configuration without rebuilding the image and persist that)

### Fixed
- Gerrit and Jenkins redirection issues when set-up behind proxy and/or using SSL
- Selenium grid link on main page. The "///" issue

## 0.3.2 - 2017-08-28
### Fixed
- SonarQube static content availability (routing)

## 0.1.0 - 2016-02-01
### Added
- First release

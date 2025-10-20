# Instagram OAuth Integration for n8n Workflows

This document describes the OAuth authentication system for Instagram posting workflows in n8n, enabling secure and user-friendly Instagram API access.

## Overview

The Instagram OAuth integration consists of two main workflows:

1. **OAuth Setup Workflow** (`instagram_oauth_setup.json`) - Handles authentication and credential generation
2. **Instagram Posting Workflow** (`instagram_post_with_oauth.json`) - Uses authenticated credentials to post content

## Workflow Architecture

### 1. OAuth Setup Workflow

**File:** `instagram_oauth_setup.json`

**Purpose:** Authenticate users with Instagram Business Account and generate access tokens.

**Flow:**
1. **Form Trigger** - Collects Facebook App credentials from user
2. **Set OAuth Parameters** - Prepares OAuth configuration
3. **Generate Auth URL** - Creates Facebook authorization URL
4. **Return Auth URL** - Sends authorization URL to user
5. **OAuth Callback Handler** - Receives authorization callback
6. **Extract Callback Data** - Processes authorization response
7. **Check for Errors** - Validates authentication success
8. **Exchange Auth Code** - Trades authorization code for access token
9. **Get Instagram Accounts** - Retrieves user's Instagram Business Accounts
10. **Set Credentials Data** - Prepares credential information
11. **Success/Error Response** - Returns authentication result

### 2. Instagram Posting Workflow

**File:** `instagram_post_with_oauth.json`

**Purpose:** Post content to Instagram using authenticated credentials.

**Flow:**
1. **Manual Trigger** - Initiates the posting process
2. **Set Post Parameters** - Configures post content and credentials
3. **Create Media Container** - Uploads media to Instagram
4. **Wait** - Allows processing time
5. **Publish Media** - Makes the post live
6. **Success Notification** - Confirms successful posting

## Authentication Requirements

### Facebook App Setup

Before using these workflows, you need:

1. **Facebook Developer Account**
   - Create account at [developers.facebook.com](https://developers.facebook.com)
   - Create a new app with "Business" type

2. **App Configuration**
   - Add "Facebook Login" product
   - Configure OAuth redirect URI
   - Set app permissions for Instagram Basic API

3. **Required Permissions**
   - `instagram_basic` - Access basic Instagram account information
   - `instagram_content_publish` - Publish content to Instagram
   - `pages_show_list` - Access Facebook pages linked to Instagram

### Instagram Business Account

- Must have an Instagram Business or Creator account
- Account must be linked to a Facebook Page
- Page must have the Instagram account connected

## Security Considerations

### Token Security
- Access tokens are stored securely using n8n's credential system
- Tokens have limited lifetime (typically 60 days)
- Implement token refresh mechanism for long-term use

### OAuth Security
- State parameter prevents CSRF attacks
- HTTPS required for all OAuth communications
- Client secret should never be exposed in client-side code

### Data Protection
- App secrets and access tokens are encrypted
- User credentials are not logged or stored in plain text
- Implement proper access controls for workflows

## Installation and Setup

### 1. Import Workflows
1. Open n8n workflow editor
2. Import `instagram_oauth_setup.json`
3. Import `instagram_post_with_oauth.json`

### 2. Configure OAuth Workflow
1. Set up webhook endpoints for OAuth callbacks
2. Configure form trigger with proper styling if needed
3. Test the authentication flow

### 3. Configure Posting Workflow
1. Set up workflow variables for credentials:
   - `INSTAGRAM_USER_ID` - Instagram Business Account ID
   - `INSTAGRAM_ACCESS_TOKEN` - OAuth access token
2. Test with sample content

### 4. Integration
1. Use OAuth workflow to generate credentials
2. Store credentials in n8n credentials system
3. Reference credentials in posting workflow

## Usage Instructions

### For End Users

1. **Authentication**
   - Access the OAuth setup form
   - Enter Facebook App credentials
   - Follow authorization flow
   - Receive confirmation of successful authentication

2. **Posting Content**
   - Use the Instagram posting workflow
   - Configure image URL and caption
   - Execute workflow to post content

### For Developers

1. **Customization**
   - Modify form fields as needed
   - Add additional error handling
   - Implement custom success/failure responses

2. **Integration**
   - Connect to external systems
   - Add content validation
   - Implement scheduling for automated posting

## Troubleshooting

### Common Issues

1. **Authentication Failures**
   - Check Facebook App configuration
   - Verify redirect URI matches
   - Ensure required permissions are granted

2. **Token Expiration**
   - Implement token refresh logic
   - Monitor token expiration dates
   - Handle re-authentication flow

3. **API Rate Limits**
   - Implement rate limiting
   - Add retry logic for failed requests
   - Monitor API usage

### Error Handling

The workflows include comprehensive error handling:
- OAuth validation errors
- API request failures
- Invalid credentials
- Network connectivity issues

## API References

### Facebook Graph API
- **Base URL:** `https://graph.facebook.com/v23.0/`
- **Documentation:** [Facebook Graph API Docs](https://developers.facebook.com/docs/graph-api)

### Instagram Basic Display API
- **Endpoints:** Media creation, publishing, account info
- **Rate Limits:** 200 requests per hour per user
- **Image Requirements:** JPG/PNG, max 8MB, aspect ratio 1.91:1 to 4:5

## Best Practices

1. **Security**
   - Regularly rotate access tokens
   - Monitor for unauthorized access
   - Use HTTPS for all communications

2. **Performance**
   - Implement caching for API responses
   - Use appropriate retry strategies
   - Monitor API usage patterns

3. **User Experience**
   - Provide clear error messages
   - Implement progress indicators
   - Offer helpful documentation

## Support and Maintenance

### Regular Maintenance
- Monitor Facebook API changes
- Update workflow versions as needed
- Test authentication flows regularly

### Scaling Considerations
- Implement load balancing for high traffic
- Consider multiple Instagram accounts
- Plan for content approval workflows

## Version History

- **v1.0** - Initial OAuth integration
- **v1.1** - Enhanced error handling
- **v1.2** - Added token refresh support

## Contributing

When modifying these workflows:
1. Test authentication flows thoroughly
2. Maintain backward compatibility
3. Update documentation for any changes
4. Follow n8n workflow best practices

---

*This documentation is part of the n8n Instagram OAuth integration system. For additional support, refer to the n8n community forums or official documentation.*
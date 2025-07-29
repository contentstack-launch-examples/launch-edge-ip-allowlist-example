# Edge IP Allowlist Example

A Next.js application demonstrating IP-based access control using Contentstack Edge Functions. This project shows how to implement IP whitelisting to restrict access to your application based on client IP addresses.

## 🚀 Features

- **IP Allowlist Protection**: Restrict access to specific IP addresses only
- **Edge Function Integration**: Uses Contentstack Edge Functions for real-time IP validation
- **Modern UI**: Beautiful, responsive interface built with Next.js and Tailwind CSS
- **Real-time Access Control**: IP validation happens at the edge for optimal performance

## 📋 Prerequisites

- Node.js 18+ 
- npm or yarn
- Contentstack account (for Edge Functions deployment)

## 🛠️ Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Edge-ip-whitelist-example-main
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to [http://localhost:3000](http://localhost:3000)

## 🔧 Configuration

### IP Whitelist Setup

Edit the `functions/[proxy].edge.js` file to configure your allowed IP addresses:

```javascript
const allowedIPs = [
  "127.0.0.1",        // Localhost
  "::1",              // IPv6 localhost
  "192.168.1.100",    // Your office IP
  "10.0.0.50",        // VPN IP
  "172.16.0.10"       // Internal network IP
];
```

### Adding Your IP Address

To add your current IP address to the whitelist:

1. Visit [whatismyipaddress.com](https://whatismyipaddress.com/) to find your public IP
2. Add it to the `allowedIPs` array in `functions/[proxy].edge.js`
3. Deploy the Edge Function

## 🏗️ Project Structure

```
Edge-ip-whitelist-example-main/
├── app/                    # Next.js app directory
│   ├── page.tsx           # Main application page
│   ├── layout.tsx         # Root layout component
│   └── globals.css        # Global styles
├── functions/
│   └── [proxy].edge.js    # Edge Function for IP validation
├── public/                # Static assets
├── package.json           # Dependencies and scripts
└── next.config.ts         # Next.js configuration
```

## 🔒 How It Works

1. **Request Interception**: All requests are intercepted by the Edge Function
2. **IP Extraction**: The client's IP address is extracted from request headers
3. **Validation**: The IP is checked against the whitelist
4. **Access Control**: 
   - ✅ **Allowed**: Request proceeds to the application
   - ❌ **Denied**: Returns 403 Forbidden response

### IP Detection Logic

The Edge Function handles various IP scenarios:
- Direct client connections
- Requests behind proxies/load balancers
- IPv4 and IPv6 addresses
- Multiple forwarded IPs

```javascript
const clientIP = request.headers.get("x-forwarded-for") || "";
const clientIPList = clientIP.split(",").map(ip => ip.trim());
```

## 🚀 Deployment

### Local Development
```bash
npm run dev
```

### Production Build
```bash
npm run build
npm start
```

### Contentstack Edge Functions

1. Deploy the Edge Function to Contentstack
2. Configure the function to intercept your desired routes
3. Test with different IP addresses

## 🧪 Testing

### Test Different IP Scenarios

1. **Allowed IP**: Should see the success page
2. **Restricted IP**: Should see "Forbidden" message
3. **Local Development**: Should work with `127.0.0.1`

### Manual Testing

You can test the IP validation by:
- Using different network connections
- Using VPN services
- Modifying the `allowedIPs` array

## 📚 Learn More

- [Contentstack Edge Functions Documentation](https://www.contentstack.com/docs/developers/launch/edge-functions)
- [Next.js Documentation](https://nextjs.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or have questions:

1. Check the [Contentstack documentation](https://www.contentstack.com/docs/)
2. Review the Edge Function logs in your Contentstack dashboard
3. Ensure your IP address is correctly added to the whitelist

---

**Note**: This is an example implementation. In production, consider additional security measures such as rate limiting, logging, and monitoring. 

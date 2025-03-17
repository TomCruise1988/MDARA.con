# MDARA.com
import React, { useState } from "react";
import { BrowserRouter as Router, Route, Routes, Link } from "react-router-dom";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { GoogleAuthProvider, signInWithPopup, getAuth } from "firebase/auth";
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);

function Home() {
  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">Liên minh Nghiên cứu Vùng Đồng bằng Sông Cửu Long</h1>
      <p className="mt-2">Hợp tác nghiên cứu và phát triển bền vững cho vùng ĐBSCL.</p>
    </div>
  );
}

function ResearchData() {
  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">Dữ liệu Nghiên cứu</h1>
      <p className="mt-2">Danh sách các nghiên cứu đã thực hiện về vùng ĐBSCL.</p>
    </div>
  );
}

function NewsEvents() {
  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">Tin tức & Sự kiện</h1>
      <p className="mt-2">Cập nhật mới nhất về các hoạt động của liên minh.</p>
    </div>
  );
}

function Library() {
  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">Thư viện Tài liệu</h1>
      <p className="mt-2">Kho tài liệu, báo cáo và nghiên cứu khoa học liên quan.</p>
      <Button className="mt-4">Tải lên tài liệu</Button>
    </div>
  );
}

function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleLogin = () => {
    alert(`Đăng nhập với Email: ${email}`);
  };

  const handleGoogleLogin = async () => {
    const provider = new GoogleAuthProvider();
    try {
      const result = await signInWithPopup(auth, provider);
      alert(`Đăng nhập thành công: ${result.user.email}`);
    } catch (error) {
      alert("Lỗi đăng nhập Google: " + error.message);
    }
  };

  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">Đăng nhập / Đăng ký</h1>
      <Input 
        type="email" 
        placeholder="Email" 
        value={email} 
        onChange={(e) => setEmail(e.target.value)} 
        className="mt-2"
      />
      <Input 
        type="password" 
        placeholder="Mật khẩu" 
        value={password} 
        onChange={(e) => setPassword(e.target.value)} 
        className="mt-2"
      />
      <Button className="mt-4" onClick={handleLogin}>Đăng nhập</Button>
      <Button className="mt-4 ml-2" onClick={handleGoogleLogin}>Đăng nhập bằng Google</Button>
    </div>
  );
}

export default function Website() {
  return (
    <Router>
      <div className="p-4">
        <nav className="mb-4 flex gap-4">
          <Link to="/">Trang chủ</Link>
          <Link to="/research">Dữ liệu Nghiên cứu</Link>
          <Link to="/news">Tin tức & Sự kiện</Link>
          <Link to="/library">Thư viện Tài liệu</Link>
          <Link to="/login">Đăng nhập</Link>
        </nav>
        <Card>
          <CardContent>
            <Routes>
              <Route path="/" element={<Home />} />
              <Route path="/research" element={<ResearchData />} />
              <Route path="/news" element={<NewsEvents />} />
              <Route path="/library" element={<Library />} />
              <Route path="/login" element={<Login />} />
            </Routes>
          </CardContent>
        </Card>
      </div>
    </Router>
  );
}

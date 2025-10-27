<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>เว็บไซต์อ่านหนังสือ (Admin Hidden Login)</title>
  <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    .admin-only { display: none; }
    .admin-active .admin-only { display: block; }
    .secret-hit { cursor: pointer; }
  </style>
</head>
<body class="bg-gray-50">
  <div id="root"></div>

  <script type="text/babel">
    function App() {
      const DEFAULT_PASS = "admin123";
      const PASS_KEY = "booksite_admin_pass_v1";
      const STORAGE_KEY = "booksite_books_v1";

      const [isAdmin, setIsAdmin] = React.useState(false);
      const [books, setBooks] = React.useState([]);
      const [query, setQuery] = React.useState("");
      const [selectedBook, setSelectedBook] = React.useState(null);
      const fileRef = React.useRef(null);
      const importRef = React.useRef(null);
      const secretHits = React.useRef([]);
      const [statusMsg, setStatusMsg] = React.useState("");

      function simpleHash(s) {
        let h = 2166136261 >>> 0;
        for (let i = 0; i < s.length; i++) {
          h ^= s.charCodeAt(i);
          h = Math.imul(h, 16777619);
        }
        return (h >>> 0).toString(16);
      }

      React.useEffect(() => {
        if (!localStorage.getItem(PASS_KEY)) {
          localStorage.setItem(PASS_KEY, simpleHash(DEFAULT_PASS));
        }
      }, []);

      React.useEffect(() => {
        const saved = localStorage.getItem(STORAGE_KEY);
        if (saved) setBooks(JSON.parse(saved));
      }, []);

      React.useEffect(() => {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(books));
      }, [books]);

      React.useEffect(() => {
        function onKey(e) {
          if (e.ctrlKey && e.shiftKey && (e.key === 'A' || e.key === 'a')) {
            activateAdminPrompt();
          }
        }
        window.addEventListener("keydown", onKey);
        return () => window.removeEventListener("keydown", onKey);
      }, []);

      function logoClicked() {
        const now = Date.now();
        secretHits.current.push(now);
        secretHits.current = secretHits.current.slice(-5);
        if (secretHits.current.length === 5 && (now - secretHits.current[0]) < 3000) {
          activateAdminPrompt();
          secretHits.current = [];
        }
      }

      function activateAdminPrompt() {
        const pw = prompt("รหัสลับ (เฉพาะแอดมิน):");
        if (pw === null) return;
        const stored = localStorage.getItem(PASS_KEY) || simpleHash(DEFAULT_PASS);
        if (simpleHash(pw) === stored) {
          setIsAdmin(true);
          setStatusMsg("เข้าสู่ระบบแอดมินเรียบร้อย");
        } else {
          alert("รหัสไม่ถูกต้อง");
        }
      }

      function changeAdminPassword() {
        const cur = prompt("ใส่รหัสปัจจุบัน:");
        if (cur === null) return;
        const stored = localStorage.getItem(PASS_KEY) || simpleHash(DEFAULT_PASS);
        if (simpleHash(cur) !== stored) {
          alert("รหัสปัจจุบันไม่ถูกต้อง");
          return;
        }
        const next = prompt("ใส่รหัสใหม่ (อย่างน้อย 6 ตัว):");
        if (!next || next.length < 6) {
          alert("รหัสใหม่สั้นเกินไป");
          return;
        }
        localStorage.setItem(PASS_KEY, simpleHash(next));
        alert("เปลี่ยนรหัสเรียบร้อย");
      }

      function handleFileUpload(e) {
        const file = e.target.files[0];
        if (!file) return;
        const reader = new FileReader();
        if (file.type.startsWith("text/") || file.name.endsWith(".md") || file.name.endsWith(".txt")) {
          reader.onload = (ev) => {
            const text = ev.target.result;
            const dataUrl = "data:text/plain;base64," + btoa(unescape(encodeURIComponent(text)));
            const newBook = {
              id: Date.now(),
              title: prompt("ชื่อหนังสือ:") || file.name,
              author: prompt("ชื่อผู้แต่ง (ถ้ามี):") || "ไม่ระบุ",
              filename: file.name,
              mime: "text/plain",
              dataUrl,
              uploadedAt: new Date().toISOString(),
            };
            setBooks((s) => [newBook, ...s]);
            setStatusMsg("อัพโหลดไฟล์ข้อความเรียบร้อย");
            fileRef.current.value = null;
          };
          reader.readAsText(file);
        } else {
          reader.onload = (ev) => {
            const dataUrl = ev.target.result;
            const newBook = {
              id: Date.now(),
              title: prompt("ชื่อหนังสือ:") || file.name,
              author: prompt("ชื่อผู้แต่ง (ถ้ามี):") || "ไม่ระบุ",
              filename: file.name,
              mime: file.type || "application/octet-stream",
              dataUrl,
              uploadedAt: new Date().toISOString(),
            };
            setBooks((s) => [newBook, ...s]);
            setStatusMsg("อัพโหลดเรียบร้อย");
            fileRef.current.value = null;
          };
          reader.readAsDataURL(file);
        }
      }

      function removeBook(id) {
        if (!confirm("ลบหนังสือจริงหรือไม่?")) return;
        setBooks((s) => s.filter((b) => b.id !== id));
        if (selectedBook && selectedBook.id === id) setSelectedBook(null);
        setStatusMsg("ลบเรียบร้อย");
      }

      function downloadBook(b) {
        const a = document.createElement("a");
        a.href = b.dataUrl;
        a.download = b.filename || (b.title + ".download");
        a.click();
      }

      function exportAllBooks() {
        const payload = {
          exportedAt: new Date().toISOString(),
          books,
        };
        const blob = new Blob([JSON.stringify(payload)], { type: "application/json" });
        const url = URL.createObjectURL(blob);
        const a = document.createElement("a");
        a.href = url;
        a.download = "books_archive.json";
        a.click();
        setStatusMsg("ส่งออกไฟล์หนังสือทั้งหมด");
      }

      function importBooksFromFile(e) {
        const f = e.target.files[0];
        if (!f) return;
        const reader = new FileReader();
        reader.onload = (ev) => {
          try {
            const obj = JSON.parse(ev.target.result);
            if (!obj.books) throw new Error("ไฟล์ไม่ตรงรูปแบบ");
            const remapped = obj.books.map(b => ({...b, id: Date.now() + Math.floor(Math.random()*1000000)}));
            setBooks((s) => [...remapped, ...s]);
            setStatusMsg("นำเข้าไฟล์หนังสือเรียบร้อย");
          } catch (err) {
            alert("ไม่สามารถอ่านไฟล์นำเข้า: " + err.message);
          }
          importRef.current.value = null;
        };
        reader.readAsText(f);
      }

      const filtered = books.filter(
        (b) =>
          b.title.toLowerCase().includes(query.toLowerCase()) ||
          b.author.toLowerCase().includes(query.toLowerCase())
      );

      return (
        <div className={(isAdmin ? "admin-active " : "") + "min-h-screen bg-gray-50 p-4 md:p-8"}>
          <header className="max-w-6xl mx-auto flex items-center justify-between">
            <div className="secret-hit" onClick={logoClicked}>
              <h1 className="text-2xl md:text-3xl font-bold">📚 เว็บไซต์อ่านหนังสือ</h1>
              <p className="text-sm text-gray-600">ระบบอัพโหลดหนังสือโดยแอดมิน — เวอร์ชันเดียวไฟล์เดียวง่ายต่อการสำรอง</p>
            </div>
            <div>
              {!isAdmin ? (
                <div className="text-sm text-gray-500">ผู้เยี่ยมชม</div>
              ) : (
                <button onClick={() => { setIsAdmin(false); setStatusMsg("ออกจากระบบแอดมิน"); }} className="px-3 py-1 rounded-lg border">ออกจากแอดมิน</button>
              )}
            </div>
          </header>

          <main className="max-w-6xl mx-auto mt-6 grid grid-cols-1 md:grid-cols-4 gap-6">
            <section className="bg-white p-4 rounded-xl shadow-sm">
              <input
                className="w-full p-2 border rounded"
                placeholder="🔍 ค้นหาหนังสือ..."
                value={query}
                onChange={(e) => setQuery(e.target.value)}
              />
              <div className="mt-4 space-y-2 max-h-[60vh] overflow-y-auto">
                {filtered.length === 0 && <div className="text-sm text-gray-500">ยังไม่มีหนังสือ</div>}
                {filtered.map((b) => (
                  <div key={b.id} className="p-2 rounded hover:bg-gray-50 flex items-center justify-between">
                    <div onClick={() => setSelectedBook(b)} className="cursor-pointer flex-1">
                      <div className="font-medium">{b.title}</div>
                      <div className="text-xs text-gray-500">{b.author}</div>
                    </div>
                    {isAdmin && <button onClick={() => removeBook(b.id)} className="text-xs px-2 py-1 border rounded admin-only">ลบ</button>}
                  </div>
                ))}
              </div>

              <div className="mt-4 admin-only">
                <label className="block text-sm font-medium">📤 อัพโหลดหนังสือ (สำหรับแอดมิน)</label>
                <input ref={fileRef} type="file" accept="application/pdf,text/*,image/*" onChange={handleFileUpload} className="mt-2" />
                <div className="mt-3 flex gap-2">
                  <button onClick={exportAllBooks} className="px-3 py-1 rounded border">ส่งออกทั้งหมด</button>
                  <label className="px-3 py-1 rounded border cursor-pointer">
                    นำเข้า
                    <input ref={importRef} onChange={importBooksFromFile} type="file" accept="application/json" className="hidden" />
                  </label>
                  <button onClick={changeAdminPassword} className="px-3 py-1 rounded border">เปลี่ยนรหัส</button>
                </div>
              </div>
            </section>

            <section className="md:col-span-3 bg-white p-4 rounded-xl shadow-sm">
              {!selectedBook && <div className="text-center text-gray-500 p-6">เลือกหนังสือจากฝั่งซ้ายเพื่อเริ่มอ่าน</div>}
              {selectedBook && (
                <div>
                  <h2 className="text-xl font-semibold">{selectedBook.title}</h2>
                  <div className="text-sm text-gray-500">{selectedBook.author}</div>
                  <div className="mt-4 border rounded p-4 bg-white">
                    {selectedBook.mime === "text/plain" && (
                      <div style={{ whiteSpace: "pre-wrap" }}>{decodeURIComponent(escape(atob(selectedBook.dataUrl.split(',')[1])))}</div>
                    )}
                    {selectedBook.mime === "application/pdf" && (
                      <iframe title={selectedBook.title} src={selectedBook.dataUrl} className="w-full h-[500px]" />
                    )}
                    {selectedBook.mime.startsWith("image/") && (
                      <img src={selectedBook.dataUrl} alt={selectedBook.title} className="w-full" />
                    )}
                  </div>
                </div>
              )}
            </section>
          </main>

          <footer className="max-w-6xl mx-auto mt-6 text-sm text-gray-500">
            <div>{statusMsg}</div>
            <div className="mt-2">เคล็ดลับ: กดหัวเรื่อง 5 ครั้งใน 3 วินาที หรือ Ctrl+Shift+A เพื่อเข้าสู่ระบบแอดมิน</div>
          </footer>
        </div>
      );
    }

    ReactDOM.createRoot(document.getElementById("root")).render(<App />);
  </script>
</body>
</html>

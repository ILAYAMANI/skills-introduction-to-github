import React, { useState, useMemo } from "react";
import {
  LayoutDashboard, Store, Package, ShoppingCart, Users, FolderTree,
  Star, CreditCard, BarChart3, Settings as SettingsIcon, Check, X,
  Search, Bell, ChevronDown, AlertCircle, TrendingUp, Clock, Ban,
  Trash2, Plus, ShieldCheck, Wallet
} from "lucide-react";
import {
  AreaChart, Area, BarChart, Bar, XAxis, YAxis, Tooltip,
  ResponsiveContainer, CartesianGrid
} from "recharts";

/* ---------------------------------- MOCK DATA ---------------------------------- */

const initialSellers = [
  { id: "SLR-1042", store: "Coastline Audio", owner: "R. Fernandes", category: "Electronics", status: "pending", joined: "2026-08-06", revenue: 0 },
  { id: "SLR-1041", store: "Verdant Home Co.", owner: "A. Krishnan", category: "Home & Living", status: "approved", joined: "2026-07-28", revenue: 184200 },
  { id: "SLR-1040", store: "Threadbare Studio", owner: "M. Okafor", category: "Apparel", status: "pending", joined: "2026-08-05", revenue: 0 },
  { id: "SLR-1039", store: "Northfold Books", owner: "S. Lindqvist", category: "Books", status: "approved", joined: "2026-06-14", revenue: 67450 },
  { id: "SLR-1038", store: "Pixel Peripherals", owner: "T. Nakamura", category: "Electronics", status: "suspended", joined: "2026-05-02", revenue: 92100 },
  { id: "SLR-1037", store: "Loam & Leaf", owner: "P. Iyer", category: "Garden", status: "approved", joined: "2026-04-19", revenue: 41200 },
  { id: "SLR-1036", store: "Ridgeline Gear", owner: "D. Correia", category: "Outdoors", status: "rejected", joined: "2026-08-01", revenue: 0 },
];

const initialProducts = [
  { id: "PRD-3081", name: "Onyx Wireless Earbuds", seller: "Pixel Peripherals", category: "Electronics", price: 3499, stock: 128, status: "active" },
  { id: "PRD-3080", name: "Handloom Cotton Throw", seller: "Verdant Home Co.", category: "Home & Living", price: 1899, stock: 42, status: "active" },
  { id: "PRD-3079", name: "Field Notes: Vol. 3", seller: "Northfold Books", category: "Books", price: 499, stock: 300, status: "active" },
  { id: "PRD-3078", name: "Merino Trail Socks (3pk)", seller: "Ridgeline Gear", category: "Outdoors", price: 899, stock: 0, status: "flagged" },
  { id: "PRD-3077", name: "Ceramic Pour-Over Set", seller: "Verdant Home Co.", category: "Home & Living", price: 2299, stock: 17, status: "active" },
  { id: "PRD-3076", name: "USB-C Fast Charger 65W", seller: "Pixel Peripherals", category: "Electronics", price: 1299, stock: 210, status: "flagged" },
];

const initialOrders = [
  { id: "ORD-88231", customer: "N. Bhatt", seller: "Verdant Home Co.", amount: 4198, status: "placed", date: "2026-08-10" },
  { id: "ORD-88230", customer: "K. Wallace", seller: "Pixel Peripherals", amount: 3499, status: "shipped", date: "2026-08-10" },
  { id: "ORD-88229", customer: "J. Moreau", seller: "Northfold Books", amount: 998, status: "delivered", date: "2026-08-09" },
  { id: "ORD-88228", customer: "A. Devi", seller: "Ridgeline Gear", amount: 899, status: "cancelled", date: "2026-08-09" },
  { id: "ORD-88227", customer: "L. Santos", seller: "Loam & Leaf", amount: 1650, status: "delivered", date: "2026-08-08" },
  { id: "ORD-88226", customer: "R. Kapoor", seller: "Verdant Home Co.", amount: 2299, status: "returned", date: "2026-08-07" },
  { id: "ORD-88225", customer: "F. Hassan", seller: "Pixel Peripherals", amount: 1299, status: "shipped", date: "2026-08-07" },
];

const initialUsers = [
  { id: "USR-5510", name: "Nisha Bhatt", email: "nisha.b@mail.com", joined: "2026-02-11", orders: 14, status: "active" },
  { id: "USR-5509", name: "Kevin Wallace", email: "kevin.w@mail.com", joined: "2026-01-30", orders: 6, status: "active" },
  { id: "USR-5508", name: "Julie Moreau", email: "julie.m@mail.com", joined: "2025-11-02", orders: 22, status: "active" },
  { id: "USR-5507", name: "Arun Devi", email: "arun.d@mail.com", joined: "2026-03-18", orders: 2, status: "blocked" },
  { id: "USR-5506", name: "Lucia Santos", email: "lucia.s@mail.com", joined: "2025-09-27", orders: 31, status: "active" },
];

const initialReviews = [
  { id: "REV-771", product: "Onyx Wireless Earbuds", user: "K. Wallace", rating: 5, comment: "Excellent bass, battery lasts all week.", status: "published" },
  { id: "REV-770", product: "Merino Trail Socks (3pk)", user: "A. Devi", rating: 1, comment: "Arrived with holes, seller ignored my message.", status: "flagged" },
  { id: "REV-769", product: "Handloom Cotton Throw", user: "R. Kapoor", rating: 4, comment: "Softer than expected, colour slightly different from photos.", status: "published" },
  { id: "REV-768", product: "USB-C Fast Charger 65W", user: "F. Hassan", rating: 2, comment: "Stopped fast-charging after two weeks.", status: "flagged" },
];

const initialCategories = [
  { id: "CAT-01", name: "Electronics", products: 214 },
  { id: "CAT-02", name: "Home & Living", products: 156 },
  { id: "CAT-03", name: "Apparel", products: 302 },
  { id: "CAT-04", name: "Books", products: 88 },
  { id: "CAT-05", name: "Garden", products: 41 },
  { id: "CAT-06", name: "Outdoors", products: 73 },
];

const payments = [
  { id: "PAY-9931", order: "ORD-88231", amount: 4198, method: "UPI", status: "success", date: "2026-08-10" },
  { id: "PAY-9930", order: "ORD-88230", amount: 3499, method: "Card", status: "success", date: "2026-08-10" },
  { id: "PAY-9929", order: "ORD-88228", amount: 899, method: "Card", status: "refunded", date: "2026-08-09" },
  { id: "PAY-9928", order: "ORD-88226", amount: 2299, method: "UPI", status: "refunded", date: "2026-08-07" },
  { id: "PAY-9927", order: "ORD-88225", amount: 1299, method: "Wallet", status: "failed", date: "2026-08-07" },
];

const revenueTrend = [
  { day: "Mon", revenue: 18200 }, { day: "Tue", revenue: 21400 }, { day: "Wed", revenue: 19800 },
  { day: "Thu", revenue: 24600 }, { day: "Fri", revenue: 28100 }, { day: "Sat", revenue: 33200 },
  { day: "Sun", revenue: 27900 },
];

const revenueByCategory = [
  { category: "Electronics", revenue: 92100 },
  { category: "Home", revenue: 78400 },
  { category: "Books", revenue: 31200 },
  { category: "Apparel", revenue: 54600 },
  { category: "Outdoors", revenue: 19800 },
];

/* ---------------------------------- HELPERS ---------------------------------- */

const STATUS_STYLES = {
  pending: { bg: "var(--accent-soft)", fg: "var(--accent)" },
  approved: { bg: "var(--success-soft)", fg: "var(--success)" },
  active: { bg: "var(--success-soft)", fg: "var(--success)" },
  published: { bg: "var(--success-soft)", fg: "var(--success)" },
  success: { bg: "var(--success-soft)", fg: "var(--success)" },
  delivered: { bg: "var(--success-soft)", fg: "var(--success)" },
  rejected: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  suspended: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  blocked: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  flagged: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  failed: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  cancelled: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  returned: { bg: "var(--danger-soft)", fg: "var(--danger)" },
  refunded: { bg: "var(--warn-soft)", fg: "var(--warn)" },
  shipped: { bg: "var(--info-soft)", fg: "var(--info)" },
  placed: { bg: "var(--info-soft)", fg: "var(--info)" },
};

function Pill({ status }) {
  const s = STATUS_STYLES[status] || { bg: "var(--panel-alt)", fg: "var(--text-muted)" };
  return (
    <span style={{
      display: "inline-flex", alignItems: "center", gap: 6,
      background: s.bg, color: s.fg, padding: "3px 10px", borderRadius: 20,
      fontFamily: "'JetBrains Mono', monospace", fontSize: 11, fontWeight: 600,
      letterSpacing: "0.03em", textTransform: "uppercase", whiteSpace: "nowrap"
    }}>
      <span style={{ width: 6, height: 6, borderRadius: "50%", background: s.fg }} />
      {status}
    </span>
  );
}

function StatCard({ label, value, delta, icon: Icon, data }) {
  return (
    <div style={{
      background: "var(--panel)", border: "1px solid var(--border)", borderRadius: 14,
      padding: "18px 20px", display: "flex", flexDirection: "column", gap: 10, minWidth: 0
    }}>
      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start" }}>
        <div>
          <div style={{
            fontFamily: "'JetBrains Mono', monospace", fontSize: 11, color: "var(--text-muted)",
            letterSpacing: "0.04em", textTransform: "uppercase"
          }}>{label}</div>
          <div style={{ fontFamily: "'Space Grotesk', sans-serif", fontSize: 26, fontWeight: 700, color: "var(--text)", marginTop: 4 }}>
            {value}
          </div>
        </div>
        <div style={{
          width: 34, height: 34, borderRadius: 9, background: "var(--accent-soft)",
          display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0
        }}>
          <Icon size={17} color="var(--accent)" />
        </div>
      </div>
      <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between" }}>
        <span style={{ fontSize: 12, color: delta >= 0 ? "var(--success)" : "var(--danger)", fontFamily: "'JetBrains Mono', monospace" }}>
          {delta >= 0 ? "▲" : "▼"} {Math.abs(delta)}%
        </span>
        {data && (
          <div style={{ width: 70, height: 24 }}>
            <ResponsiveContainer width="100%" height="100%">
              <AreaChart data={data}>
                <Area type="monotone" dataKey="revenue" stroke="var(--accent)" fill="var(--accent-soft)" strokeWidth={1.5} />
              </AreaChart>
            </ResponsiveContainer>
          </div>
        )}
      </div>
    </div>
  );
}

function Panel({ title, subtitle, right, children }) {
  return (
    <div style={{ background: "var(--panel)", border: "1px solid var(--border)", borderRadius: 14, overflow: "hidden" }}>
      <div style={{
        padding: "16px 20px", borderBottom: "1px solid var(--border)",
        display: "flex", justifyContent: "space-between", alignItems: "center"
      }}>
        <div>
          <div style={{ fontFamily: "'Space Grotesk', sans-serif", fontWeight: 600, fontSize: 15, color: "var(--text)" }}>{title}</div>
          {subtitle && <div style={{ fontSize: 12, color: "var(--text-muted)", marginTop: 2 }}>{subtitle}</div>}
        </div>
        {right}
      </div>
      {children}
    </div>
  );
}

function IconBtn({ onClick, color, children, title }) {
  return (
    <button onClick={onClick} title={title} style={{
      display: "inline-flex", alignItems: "center", justifyContent: "center",
      width: 28, height: 28, borderRadius: 7, border: "1px solid var(--border)",
      background: "var(--panel-alt)", color, cursor: "pointer"
    }}>
      {children}
    </button>
  );
}

const th = {
  textAlign: "left", padding: "10px 20px", fontFamily: "'JetBrains Mono', monospace",
  fontSize: 10.5, color: "var(--text-muted)", letterSpacing: "0.05em", textTransform: "uppercase",
  borderBottom: "1px solid var(--border)"
};
const td = { padding: "13px 20px", fontSize: 13.5, color: "var(--text)", borderBottom: "1px solid var(--border)" };
const mono = { fontFamily: "'JetBrains Mono', monospace", fontSize: 12.5, color: "var(--text-muted)" };

/* ---------------------------------- NAV ---------------------------------- */

const NAV = [
  { id: "dashboard", label: "Dashboard", icon: LayoutDashboard },
  { id: "users", label: "Users", icon: Users },
  { id: "sellers", label: "Sellers", icon: Store },
  { id: "products", label: "Products", icon: Package },
  { id: "categories", label: "Categories", icon: FolderTree },
  { id: "orders", label: "Orders", icon: ShoppingCart },
  { id: "payments", label: "Payments", icon: CreditCard },
  { id: "reviews", label: "Reviews", icon: Star },
  { id: "reports", label: "Reports", icon: BarChart3 },
  { id: "settings", label: "Settings", icon: SettingsIcon },
];

/* ---------------------------------- APP ---------------------------------- */

export default function AdminPortal() {
  const [tab, setTab] = useState("dashboard");
  const [sellers, setSellers] = useState(initialSellers);
  const [products, setProducts] = useState(initialProducts);
  const [orders, setOrders] = useState(initialOrders);
  const [users, setUsers] = useState(initialUsers);
  const [reviews, setReviews] = useState(initialReviews);
  const [categories, setCategories] = useState(initialCategories);
  const [newCategory, setNewCategory] = useState("");
  const [sellerFilter, setSellerFilter] = useState("all");
  const [orderFilter, setOrderFilter] = useState("all");
  const [productQuery, setProductQuery] = useState("");
  const [settings, setSettings] = useState({ siteName: "Vendly", commission: 8, supportEmail: "support@vendly.example" });
  const [savedFlash, setSavedFlash] = useState(false);

  const pendingSellers = sellers.filter(s => s.status === "pending").length;
  const flaggedReviews = reviews.filter(r => r.status === "flagged").length;
  const totalRevenue = orders.filter(o => o.status !== "cancelled" && o.status !== "returned").reduce((a, o) => a + o.amount, 0);
  const ordersToday = orders.filter(o => o.date === "2026-08-10").length;
  const activeSellers = sellers.filter(s => s.status === "approved").length;

  const setSellerStatus = (id, status) => setSellers(prev => prev.map(s => s.id === id ? { ...s, status } : s));
  const setOrderStatus = (id, status) => setOrders(prev => prev.map(o => o.id === id ? { ...o, status } : o));
  const setUserStatus = (id, status) => setUsers(prev => prev.map(u => u.id === id ? { ...u, status } : u));
  const setReviewStatus = (id, status) => setReviews(prev => prev.map(r => r.id === id ? { ...r, status } : r));
  const toggleProductFlag = (id) => setProducts(prev => prev.map(p => p.id === id ? { ...p, status: p.status === "flagged" ? "active" : "flagged" } : p));
  const removeCategory = (id) => setCategories(prev => prev.filter(c => c.id !== id));
  const addCategory = () => {
    if (!newCategory.trim()) return;
    setCategories(prev => [...prev, { id: `CAT-${String(prev.length + 1).padStart(2, "0")}`, name: newCategory.trim(), products: 0 }]);
    setNewCategory("");
  };

  const filteredSellers = sellerFilter === "all" ? sellers : sellers.filter(s => s.status === sellerFilter);
  const filteredOrders = orderFilter === "all" ? orders : orders.filter(o => o.status === orderFilter);
  const filteredProducts = products.filter(p => p.name.toLowerCase().includes(productQuery.toLowerCase()) || p.seller.toLowerCase().includes(productQuery.toLowerCase()));

  const currentNav = NAV.find(n => n.id === tab);

  return (
    <div style={{
      "--bg": "#0F1720", "--panel": "#161F2C", "--panel-alt": "#1C2632",
      "--border": "#293544", "--text": "#EDEFF2", "--text-muted": "#8B96A5",
      "--accent": "#E8A33D", "--accent-soft": "rgba(232,163,61,0.15)",
      "--success": "#4CAF7D", "--success-soft": "rgba(76,175,125,0.15)",
      "--danger": "#E2574C", "--danger-soft": "rgba(226,87,76,0.15)",
      "--warn": "#D9A441", "--warn-soft": "rgba(217,164,65,0.13)",
      "--info": "#5B9BD5", "--info-soft": "rgba(91,155,213,0.15)",
      background: "var(--bg)", minHeight: "100vh", color: "var(--text)",
      fontFamily: "'Inter', sans-serif", display: "flex"
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500;600&display=swap');
        * { box-sizing: border-box; }
        table { width: 100%; border-collapse: collapse; }
        button { font-family: inherit; }
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
      `}</style>

      {/* SIDEBAR */}
      <div style={{
        width: 236, flexShrink: 0, borderRight: "1px solid var(--border)",
        display: "flex", flexDirection: "column", padding: "20px 14px", position: "sticky", top: 0, height: "100vh"
      }}>
        <div style={{ display: "flex", alignItems: "center", gap: 9, padding: "0 8px 22px" }}>
          <div style={{
            width: 30, height: 30, borderRadius: 8, background: "var(--accent)",
            display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "'Space Grotesk', sans-serif",
            fontWeight: 700, color: "#0F1720", fontSize: 15
          }}>V</div>
          <div style={{ fontFamily: "'Space Grotesk', sans-serif", fontWeight: 700, fontSize: 16, letterSpacing: "-0.01em" }}>
            Vendly <span style={{ color: "var(--text-muted)", fontWeight: 500 }}>Admin</span>
          </div>
        </div>

        <div style={{ display: "flex", flexDirection: "column", gap: 2, flex: 1 }}>
          {NAV.map(item => {
            const Icon = item.icon;
            const activeItem = tab === item.id;
            const badge = item.id === "sellers" ? pendingSellers : item.id === "reviews" ? flaggedReviews : 0;
            return (
              <button key={item.id} onClick={() => setTab(item.id)} style={{
                display: "flex", alignItems: "center", gap: 10, padding: "9px 12px", borderRadius: 9,
                border: "none", cursor: "pointer", textAlign: "left",
                background: activeItem ? "var(--accent-soft)" : "transparent",
                color: activeItem ? "var(--accent)" : "var(--text-muted)",
                fontSize: 13.5, fontWeight: activeItem ? 600 : 500
              }}>
                <Icon size={16} />
                <span style={{ flex: 1 }}>{item.label}</span>
                {badge > 0 && (
                  <span style={{
                    background: "var(--danger)", color: "#fff", fontSize: 10, fontWeight: 700,
                    borderRadius: 10, padding: "1px 6px", fontFamily: "'JetBrains Mono', monospace"
                  }}>{badge}</span>
                )}
              </button>
            );
          })}
        </div>

        <div style={{
          borderTop: "1px solid var(--border)", paddingTop: 14, display: "flex", alignItems: "center", gap: 8
        }}>
          <span style={{ width: 7, height: 7, borderRadius: "50%", background: "var(--success)" }} />
          <span style={{ fontFamily: "'JetBrains Mono', monospace", fontSize: 10.5, color: "var(--text-muted)", letterSpacing: "0.03em" }}>
            ALL_SYSTEMS_NOMINAL
          </span>
        </div>
      </div>

      {/* MAIN */}
      <div style={{ flex: 1, minWidth: 0 }}>
        {/* TOPBAR */}
        <div style={{
          height: 62, borderBottom: "1px solid var(--border)", display: "flex", alignItems: "center",
          justifyContent: "space-between", padding: "0 24px", position: "sticky", top: 0, background: "var(--bg)", zIndex: 5
        }}>
          <div style={{ fontFamily: "'Space Grotesk', sans-serif", fontWeight: 600, fontSize: 17 }}>{currentNav.label}</div>
          <div style={{ display: "flex", alignItems: "center", gap: 14 }}>
            <div style={{
              display: "flex", alignItems: "center", gap: 8, background: "var(--panel)",
              border: "1px solid var(--border)", borderRadius: 9, padding: "7px 12px", width: 240
            }}>
              <Search size={14} color="var(--text-muted)" />
              <input placeholder="Search…" style={{
                background: "transparent", border: "none", outline: "none", color: "var(--text)", fontSize: 13, width: "100%"
              }} />
            </div>
            <IconBtn color="var(--text-muted)"><Bell size={15} /></IconBtn>
            <div style={{
              width: 32, height: 32, borderRadius: "50%", background: "var(--accent-soft)", color: "var(--accent)",
              display: "flex", alignItems: "center", justifyContent: "center", fontSize: 12, fontWeight: 700,
              fontFamily: "'Space Grotesk', sans-serif"
            }}>AD</div>
          </div>
        </div>

        <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>

          {/* DASHBOARD */}
          {tab === "dashboard" && (
            <>
              <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 16 }}>
                <StatCard label="Revenue_24h" value={`₹${totalRevenue.toLocaleString("en-IN")}`} delta={12} icon={TrendingUp} data={revenueTrend} />
                <StatCard label="Orders_Today" value={ordersToday} delta={4} icon={ShoppingCart} />
                <StatCard label="Active_Sellers" value={activeSellers} delta={2} icon={Store} />
                <StatCard label="Pending_Approval" value={pendingSellers} delta={-1} icon={Clock} />
              </div>

              <Panel title="Revenue — last 7 days" subtitle="Gross merchandise value, all sellers">
                <div style={{ padding: "16px 20px", height: 220 }}>
                  <ResponsiveContainer width="100%" height="100%">
                    <AreaChart data={revenueTrend}>
                      <CartesianGrid strokeDasharray="3 3" stroke="var(--border)" vertical={false} />
                      <XAxis dataKey="day" stroke="var(--text-muted)" fontSize={11.5} tickLine={false} axisLine={false} />
                      <YAxis stroke="var(--text-muted)" fontSize={11.5} tickLine={false} axisLine={false} width={50} />
                      <Tooltip contentStyle={{ background: "var(--panel-alt)", border: "1px solid var(--border)", borderRadius: 8, fontSize: 12 }} />
                      <Area type="monotone" dataKey="revenue" stroke="var(--accent)" fill="var(--accent-soft)" strokeWidth={2} />
                    </AreaChart>
                  </ResponsiveContainer>
                </div>
              </Panel>

              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
                <Panel title="Seller approval queue" subtitle={`${pendingSellers} pending review`}>
                  <div>
                    {sellers.filter(s => s.status === "pending").map(s => (
                      <div key={s.id} style={{
                        display: "flex", alignItems: "center", justifyContent: "space-between",
                        padding: "12px 20px", borderBottom: "1px solid var(--border)"
                      }}>
                        <div>
                          <div style={{ fontSize: 13.5, fontWeight: 600 }}>{s.store}</div>
                          <div style={{ ...mono, marginTop: 2 }}>{s.id} · {s.category}</div>
                        </div>
                        <div style={{ display: "flex", gap: 6 }}>
                          <IconBtn color="var(--success)" title="Approve" onClick={() => setSellerStatus(s.id, "approved")}><Check size={14} /></IconBtn>
                          <IconBtn color="var(--danger)" title="Reject" onClick={() => setSellerStatus(s.id, "rejected")}><X size={14} /></IconBtn>
                        </div>
                      </div>
                    ))}
                    {pendingSellers === 0 && <div style={{ padding: 20, fontSize: 13, color: "var(--text-muted)" }}>Queue is clear.</div>}
                  </div>
                </Panel>

                <Panel title="Recent orders" subtitle="Latest activity across the marketplace">
                  <div>
                    {orders.slice(0, 5).map(o => (
                      <div key={o.id} style={{
                        display: "flex", alignItems: "center", justifyContent: "space-between",
                        padding: "12px 20px", borderBottom: "1px solid var(--border)"
                      }}>
                        <div>
                          <div style={{ fontSize: 13.5, fontWeight: 600 }}>{o.customer}</div>
                          <div style={{ ...mono, marginTop: 2 }}>{o.id} · ₹{o.amount.toLocaleString("en-IN")}</div>
                        </div>
                        <Pill status={o.status} />
                      </div>
                    ))}
                  </div>
                </Panel>
              </div>
            </>
          )}

          {/* USERS */}
          {tab === "users" && (
            <Panel title="Users" subtitle={`${users.length} registered`}>
              <table>
                <thead><tr>
                  <th style={th}>Name</th><th style={th}>Email</th><th style={th}>Joined</th>
                  <th style={th}>Orders</th><th style={th}>Status</th><th style={th}></th>
                </tr></thead>
                <tbody>
                  {users.map(u => (
                    <tr key={u.id}>
                      <td style={td}><div style={{ fontWeight: 600 }}>{u.name}</div><div style={mono}>{u.id}</div></td>
                      <td style={{ ...td, color: "var(--text-muted)" }}>{u.email}</td>
                      <td style={{ ...td, ...mono }}>{u.joined}</td>
                      <td style={td}>{u.orders}</td>
                      <td style={td}><Pill status={u.status} /></td>
                      <td style={td}>
                        {u.status === "active" ? (
                          <IconBtn color="var(--danger)" title="Block" onClick={() => setUserStatus(u.id, "blocked")}><Ban size={14} /></IconBtn>
                        ) : (
                          <IconBtn color="var(--success)" title="Unblock" onClick={() => setUserStatus(u.id, "active")}><Check size={14} /></IconBtn>
                        )}
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* SELLERS */}
          {tab === "sellers" && (
            <Panel title="Sellers" subtitle={`${sellers.length} total`} right={
              <div style={{ display: "flex", gap: 6 }}>
                {["all", "pending", "approved", "rejected", "suspended"].map(f => (
                  <button key={f} onClick={() => setSellerFilter(f)} style={{
                    padding: "6px 12px", borderRadius: 7, border: "1px solid var(--border)", cursor: "pointer",
                    background: sellerFilter === f ? "var(--accent-soft)" : "var(--panel-alt)",
                    color: sellerFilter === f ? "var(--accent)" : "var(--text-muted)",
                    fontSize: 12, fontWeight: 600, textTransform: "capitalize"
                  }}>{f}</button>
                ))}
              </div>
            }>
              <table>
                <thead><tr>
                  <th style={th}>Store</th><th style={th}>Owner</th><th style={th}>Category</th>
                  <th style={th}>Joined</th><th style={th}>Revenue</th><th style={th}>Status</th><th style={th}></th>
                </tr></thead>
                <tbody>
                  {filteredSellers.map(s => (
                    <tr key={s.id}>
                      <td style={td}><div style={{ fontWeight: 600 }}>{s.store}</div><div style={mono}>{s.id}</div></td>
                      <td style={{ ...td, color: "var(--text-muted)" }}>{s.owner}</td>
                      <td style={td}>{s.category}</td>
                      <td style={{ ...td, ...mono }}>{s.joined}</td>
                      <td style={{ ...td, ...mono }}>₹{s.revenue.toLocaleString("en-IN")}</td>
                      <td style={td}><Pill status={s.status} /></td>
                      <td style={td}>
                        <div style={{ display: "flex", gap: 6 }}>
                          {s.status === "pending" && <>
                            <IconBtn color="var(--success)" title="Approve" onClick={() => setSellerStatus(s.id, "approved")}><Check size={14} /></IconBtn>
                            <IconBtn color="var(--danger)" title="Reject" onClick={() => setSellerStatus(s.id, "rejected")}><X size={14} /></IconBtn>
                          </>}
                          {s.status === "approved" && (
                            <IconBtn color="var(--danger)" title="Suspend" onClick={() => setSellerStatus(s.id, "suspended")}><Ban size={14} /></IconBtn>
                          )}
                          {s.status === "suspended" && (
                            <IconBtn color="var(--success)" title="Reinstate" onClick={() => setSellerStatus(s.id, "approved")}><ShieldCheck size={14} /></IconBtn>
                          )}
                        </div>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* PRODUCTS */}
          {tab === "products" && (
            <Panel title="Products" subtitle={`${products.length} listed`} right={
              <div style={{
                display: "flex", alignItems: "center", gap: 8, background: "var(--panel-alt)",
                border: "1px solid var(--border)", borderRadius: 8, padding: "6px 10px", width: 220
              }}>
                <Search size={13} color="var(--text-muted)" />
                <input value={productQuery} onChange={e => setProductQuery(e.target.value)} placeholder="Filter products…" style={{
                  background: "transparent", border: "none", outline: "none", color: "var(--text)", fontSize: 12.5, width: "100%"
                }} />
              </div>
            }>
              <table>
                <thead><tr>
                  <th style={th}>Product</th><th style={th}>Seller</th><th style={th}>Category</th>
                  <th style={th}>Price</th><th style={th}>Stock</th><th style={th}>Status</th><th style={th}></th>
                </tr></thead>
                <tbody>
                  {filteredProducts.map(p => (
                    <tr key={p.id}>
                      <td style={td}><div style={{ fontWeight: 600 }}>{p.name}</div><div style={mono}>{p.id}</div></td>
                      <td style={{ ...td, color: "var(--text-muted)" }}>{p.seller}</td>
                      <td style={td}>{p.category}</td>
                      <td style={{ ...td, ...mono }}>₹{p.price.toLocaleString("en-IN")}</td>
                      <td style={{ ...td, ...mono, color: p.stock === 0 ? "var(--danger)" : "var(--text)" }}>{p.stock}</td>
                      <td style={td}><Pill status={p.status} /></td>
                      <td style={td}>
                        <IconBtn color={p.status === "flagged" ? "var(--success)" : "var(--danger)"}
                          title={p.status === "flagged" ? "Unflag" : "Flag"} onClick={() => toggleProductFlag(p.id)}>
                          {p.status === "flagged" ? <Check size={14} /> : <AlertCircle size={14} />}
                        </IconBtn>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* CATEGORIES */}
          {tab === "categories" && (
            <Panel title="Categories" subtitle={`${categories.length} active`} right={
              <div style={{ display: "flex", gap: 8 }}>
                <input value={newCategory} onChange={e => setNewCategory(e.target.value)} placeholder="New category name"
                  onKeyDown={e => e.key === "Enter" && addCategory()}
                  style={{
                    background: "var(--panel-alt)", border: "1px solid var(--border)", borderRadius: 8,
                    padding: "6px 10px", color: "var(--text)", fontSize: 12.5, outline: "none", width: 180
                  }} />
                <button onClick={addCategory} style={{
                  display: "flex", alignItems: "center", gap: 5, background: "var(--accent)", color: "#0F1720",
                  border: "none", borderRadius: 8, padding: "6px 12px", fontSize: 12.5, fontWeight: 700, cursor: "pointer"
                }}><Plus size={13} /> Add</button>
              </div>
            }>
              <table>
                <thead><tr><th style={th}>Category</th><th style={th}>Products</th><th style={th}></th></tr></thead>
                <tbody>
                  {categories.map(c => (
                    <tr key={c.id}>
                      <td style={td}><div style={{ fontWeight: 600 }}>{c.name}</div><div style={mono}>{c.id}</div></td>
                      <td style={{ ...td, ...mono }}>{c.products}</td>
                      <td style={td}><IconBtn color="var(--danger)" title="Delete" onClick={() => removeCategory(c.id)}><Trash2 size={14} /></IconBtn></td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* ORDERS */}
          {tab === "orders" && (
            <Panel title="Orders" subtitle={`${orders.length} total`} right={
              <div style={{ display: "flex", gap: 6, flexWrap: "wrap" }}>
                {["all", "placed", "shipped", "delivered", "cancelled", "returned"].map(f => (
                  <button key={f} onClick={() => setOrderFilter(f)} style={{
                    padding: "6px 12px", borderRadius: 7, border: "1px solid var(--border)", cursor: "pointer",
                    background: orderFilter === f ? "var(--accent-soft)" : "var(--panel-alt)",
                    color: orderFilter === f ? "var(--accent)" : "var(--text-muted)",
                    fontSize: 12, fontWeight: 600, textTransform: "capitalize"
                  }}>{f}</button>
                ))}
              </div>
            }>
              <table>
                <thead><tr>
                  <th style={th}>Order</th><th style={th}>Customer</th><th style={th}>Seller</th>
                  <th style={th}>Amount</th><th style={th}>Date</th><th style={th}>Status</th>
                </tr></thead>
                <tbody>
                  {filteredOrders.map(o => (
                    <tr key={o.id}>
                      <td style={{ ...td, ...mono }}>{o.id}</td>
                      <td style={td}>{o.customer}</td>
                      <td style={{ ...td, color: "var(--text-muted)" }}>{o.seller}</td>
                      <td style={{ ...td, ...mono }}>₹{o.amount.toLocaleString("en-IN")}</td>
                      <td style={{ ...td, ...mono }}>{o.date}</td>
                      <td style={td}>
                        <select value={o.status} onChange={e => setOrderStatus(o.id, e.target.value)} style={{
                          background: "var(--panel-alt)", color: "var(--text)", border: "1px solid var(--border)",
                          borderRadius: 7, padding: "5px 8px", fontSize: 12, fontFamily: "'JetBrains Mono', monospace"
                        }}>
                          {["placed", "shipped", "delivered", "cancelled", "returned"].map(s => <option key={s} value={s}>{s}</option>)}
                        </select>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* PAYMENTS */}
          {tab === "payments" && (
            <Panel title="Payments" subtitle={`${payments.length} transactions`}>
              <table>
                <thead><tr>
                  <th style={th}>Payment</th><th style={th}>Order</th><th style={th}>Amount</th>
                  <th style={th}>Method</th><th style={th}>Date</th><th style={th}>Status</th>
                </tr></thead>
                <tbody>
                  {payments.map(p => (
                    <tr key={p.id}>
                      <td style={{ ...td, ...mono }}>{p.id}</td>
                      <td style={{ ...td, ...mono, color: "var(--text-muted)" }}>{p.order}</td>
                      <td style={{ ...td, ...mono }}>₹{p.amount.toLocaleString("en-IN")}</td>
                      <td style={td}>{p.method}</td>
                      <td style={{ ...td, ...mono }}>{p.date}</td>
                      <td style={td}><Pill status={p.status} /></td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </Panel>
          )}

          {/* REVIEWS */}
          {tab === "reviews" && (
            <Panel title="Reviews" subtitle={`${flaggedReviews} flagged for moderation`}>
              <div>
                {reviews.map(r => (
                  <div key={r.id} style={{ padding: "14px 20px", borderBottom: "1px solid var(--border)" }}>
                    <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start" }}>
                      <div>
                        <div style={{ fontWeight: 600, fontSize: 13.5 }}>{r.product}</div>
                        <div style={{ ...mono, marginTop: 2 }}>{r.id} · {r.user}</div>
                      </div>
                      <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                        <span style={{ color: "var(--accent)", fontSize: 13, display: "flex", gap: 2 }}>
                          {Array.from({ length: 5 }).map((_, i) => (
                            <Star key={i} size={13} fill={i < r.rating ? "var(--accent)" : "none"} color="var(--accent)" />
                          ))}
                        </span>
                        <Pill status={r.status} />
                      </div>
                    </div>
                    <div style={{ fontSize: 13, color: "var(--text-muted)", marginTop: 8, maxWidth: 640 }}>{r.comment}</div>
                    {r.status === "flagged" && (
                      <div style={{ display: "flex", gap: 8, marginTop: 10 }}>
                        <button onClick={() => setReviewStatus(r.id, "published")} style={{
                          background: "var(--success-soft)", color: "var(--success)", border: "none",
                          borderRadius: 7, padding: "5px 12px", fontSize: 12, fontWeight: 600, cursor: "pointer"
                        }}>Approve</button>
                        <button onClick={() => setReviewStatus(r.id, "removed")} style={{
                          background: "var(--danger-soft)", color: "var(--danger)", border: "none",
                          borderRadius: 7, padding: "5px 12px", fontSize: 12, fontWeight: 600, cursor: "pointer"
                        }}>Remove</button>
                      </div>
                    )}
                  </div>
                ))}
              </div>
            </Panel>
          )}

          {/* REPORTS */}
          {tab === "reports" && (
            <>
              <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 16 }}>
                <StatCard label="GMV_7d" value={`₹${revenueTrend.reduce((a, d) => a + d.revenue, 0).toLocaleString("en-IN")}`} delta={9} icon={Wallet} />
                <StatCard label="Avg_Order_Value" value={`₹${Math.round(totalRevenue / orders.length).toLocaleString("en-IN")}`} delta={3} icon={TrendingUp} />
                <StatCard label="Return_Rate" value="6.4%" delta={-1} icon={AlertCircle} />
              </div>
              <Panel title="Revenue by category" subtitle="Trailing 30 days">
                <div style={{ padding: "16px 20px", height: 240 }}>
                  <ResponsiveContainer width="100%" height="100%">
                    <BarChart data={revenueByCategory}>
                      <CartesianGrid strokeDasharray="3 3" stroke="var(--border)" vertical={false} />
                      <XAxis dataKey="category" stroke="var(--text-muted)" fontSize={11.5} tickLine={false} axisLine={false} />
                      <YAxis stroke="var(--text-muted)" fontSize={11.5} tickLine={false} axisLine={false} width={50} />
                      <Tooltip contentStyle={{ background: "var(--panel-alt)", border: "1px solid var(--border)", borderRadius: 8, fontSize: 12 }} />
                      <Bar dataKey="revenue" fill="var(--accent)" radius={[5, 5, 0, 0]} />
                    </BarChart>
                  </ResponsiveContainer>
                </div>
              </Panel>
            </>
          )}

          {/* SETTINGS */}
          {tab === "settings" && (
            <Panel title="Website settings" subtitle="Global marketplace configuration">
              <div style={{ padding: 20, display: "flex", flexDirection: "column", gap: 16, maxWidth: 420 }}>
                {[
                  { key: "siteName", label: "Site name" },
                  { key: "commission", label: "Commission (%)" },
                  { key: "supportEmail", label: "Support email" },
                ].map(f => (
                  <div key={f.key} style={{ display: "flex", flexDirection: "column", gap: 6 }}>
                    <label style={{ fontSize: 12, color: "var(--text-muted)", fontFamily: "'JetBrains Mono', monospace", textTransform: "uppercase", letterSpacing: "0.03em" }}>
                      {f.label}
                    </label>
                    <input value={settings[f.key]} onChange={e => setSettings(s => ({ ...s, [f.key]: e.target.value }))} style={{
                      background: "var(--panel-alt)", border: "1px solid var(--border)", borderRadius: 8,
                      padding: "9px 12px", color: "var(--text)", fontSize: 13.5, outline: "none"
                    }} />
                  </div>
                ))}
                <button onClick={() => { setSavedFlash(true); setTimeout(() => setSavedFlash(false), 1800); }} style={{
                  alignSelf: "flex-start", background: "var(--accent)", color: "#0F1720", border: "none",
                  borderRadius: 8, padding: "9px 18px", fontSize: 13, fontWeight: 700, cursor: "pointer", marginTop: 4
                }}>Save changes</button>
                {savedFlash && <div style={{ fontSize: 12.5, color: "var(--success)" }}>Settings saved.</div>}
              </div>
            </Panel>
          )}

        </div>
      </div>
    </div>
  );
}

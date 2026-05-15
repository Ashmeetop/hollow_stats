import React, { useState, useEffect, useRef } from 'react';
import {
  ThemeProvider,
  createTheme,
  Container,
  Card,
  CardContent,
  Typography,
  Grid,
  Box,
  Paper,
} from '@mui/material';
import { initializeApp } from 'https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js';
import {
  getDatabase,
  ref,
  onValue,
  set,
} from 'https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js';

const darkTheme = createTheme({
  palette: {
    mode: 'dark',
    background: {
      default: '#000000',
      paper: '#1c1c1e',
    },
    primary: {
      main: '#ffffff',
    },
    secondary: {
      main: '#98989f',
    },
  },
  typography: {
    fontFamily: [
      '-apple-system',
      'BlinkMacSystemFont',
      '"Segoe UI"',
      'Roboto',
      'sans-serif',
    ].join(','),
    h1: {
      fontSize: '3.5rem',
      fontWeight: 600,
      fontFamily: 'ui-monospace, SFMono-Regular, Menlo, monospace',
    },
    h3: {
      fontSize: '1.75rem',
      fontWeight: 600,
      fontFamily: 'ui-monospace, SFMono-Regular, Menlo, monospace',
    },
    subtitle2: {
      fontSize: '0.813rem',
      color: '#98989f',
      textTransform: 'uppercase',
      letterSpacing: '0.5px',
    },
    body2: {
      fontSize: '0.875rem',
      color: '#98989f',
    },
  },
  components: {
    MuiCard: {
      styleOverrides: {
        root: {
          backgroundColor: '#1c1c1e',
          borderRadius: '24px',
          border: 'none',
        },
      },
    },
    MuiPaper: {
      styleOverrides: {
        root: {
          backgroundColor: '#1c1c1e',
          borderRadius: '16px',
        },
      },
    },
  },
});

const firebaseConfig = {
  apiKey: 'AIzaSyBImlfiRQOoY5kWBU-YsSffKEYTjFJdDe8',
  authDomain: 'hollow-launcher-api.firebaseapp.com',
  databaseURL: 'https://hollow-launcher-api-default-rtdb.asia-southeast1.firebasedatabase.app',
  projectId: 'hollow-launcher-api',
  storageBucket: 'hollow-launcher-api.firebasestorage.app',
  messagingSenderId: '981071558548',
  appId: '1:981071558548:web:df8bcde1e1fd0a2cb80181',
  measurementId: 'G-W6DM9YCQM4',
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

const ACTIVE_WINDOW = 5 * 60 * 1000;

function getStartOfDay(date = new Date()) {
  const d = new Date(date);
  d.setHours(0, 0, 0, 0);
  return d.getTime();
}

function getStartOfWeek(date = new Date()) {
  const d = new Date(date);
  const day = d.getDay();
  const diff = d.getDate() - day;
  const startDate = new Date(d.setDate(diff));
  startDate.setHours(0, 0, 0, 0);
  return startDate.getTime();
}

function getStartOfMonth(date = new Date()) {
  const d = new Date(date);
  d.setDate(1);
  d.setHours(0, 0, 0, 0);
  return d.getTime();
}

function HollowDashboard() {
  const [activeNow, setActiveNow] = useState(0);
  const [peakToday, setPeakToday] = useState(0);
  const [peakAlltime, setPeakAlltime] = useState(0);
  const [today, setToday] = useState(0);
  const [week, setWeek] = useState(0);
  const [month, setMonth] = useState(0);
  const [alltime, setAlltime] = useState(0);
  const [versions, setVersions] = useState([]);
  const [history, setHistory] = useState(Array(30).fill(0));
  const canvasRef = useRef(null);

  const lastPeakResetRef = useRef(new Date().toDateString());
  const peakTodayRef = useRef(0);
  const peakAlltimeRef = useRef(0);

  useEffect(() => {
    const unsubscribe = onValue(ref(db, 'players'), (snap) => {
      const now = Date.now();
      const boundaries = {
        today: getStartOfDay(),
        week: getStartOfWeek(),
        month: getStartOfMonth(),
      };

      const todayString = new Date().toDateString();
      if (todayString !== lastPeakResetRef.current) {
        lastPeakResetRef.current = todayString;
        peakTodayRef.current = 0;
      }

      let active = 0;
      let todayCount = 0;
      let weekCount = 0;
      let monthCount = 0;
      let alltimeCount = 0;
      const versionMap = {};

      if (snap.exists()) {
        snap.forEach((child) => {
          const data = child.val();
          if (!data) return;

          const ts = data.lastSeen;
          if (typeof ts !== 'number') return;

          alltimeCount++;

          if (ts >= boundaries.today) todayCount++;
          if (ts >= boundaries.week) weekCount++;
          if (ts >= boundaries.month) monthCount++;

          if (now - ts <= ACTIVE_WINDOW) {
            active++;
          }

          const version = data.version || 'Unknown';
          versionMap[version] = (versionMap[version] || 0) + 1;
        });
      }

      setHistory((prev) => {
        const newHistory = [...prev];
        newHistory.shift();
        newHistory.push(active);
        return newHistory;
      });

      if (active > peakAlltimeRef.current) {
        peakAlltimeRef.current = active;
        setPeakAlltime(active);
        set(ref(db, 'metadata/peakAlltime'), active);
      }

      if (active > peakTodayRef.current) {
        peakTodayRef.current = active;
        setPeakToday(active);
        set(ref(db, 'metadata/peakToday'), active);
      }

      setActiveNow(active);
      setToday(todayCount);
      setWeek(weekCount);
      setMonth(monthCount);
      setAlltime(alltimeCount);

      const sortedVersions = Object.entries(versionMap)
        .sort((a, b) => b[1] - a[1])
        .map(([version, count]) => ({ version, count }));

      setVersions(sortedVersions);
    });

    return () => unsubscribe();
  }, []);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    const w = (canvas.width = canvas.offsetWidth);
    const h = 120;

    ctx.clearRect(0, 0, w, h);

    const max = Math.max(...history, 1);

    ctx.beginPath();
    history.forEach((v, i) => {
      const x = (i / (history.length - 1)) * w;
      const y = h - (v / max) * (h - 10);

      if (i === 0) {
        ctx.moveTo(x, y);
      } else {
        ctx.lineTo(x, y);
      }
    });

    ctx.strokeStyle = '#ffffff';
    ctx.lineWidth = 2;
    ctx.lineCap = 'round';
    ctx.lineJoin = 'round';
    ctx.stroke();
  }, [history]);

  return (
    <ThemeProvider theme={darkTheme}>
      <Box sx={{ backgroundColor: '#000000', minHeight: '100vh', py: 3 }}>
        <Container maxWidth="sm">
          <Typography
            variant="h1"
            sx={{
              mb: 3,
              fontSize: { xs: '2.5rem', sm: '3.5rem' },
              fontWeight: 600,
            }}
          >
            Dashboard
          </Typography>

          <Card sx={{ mb: 2 }}>
            <CardContent>
              <Typography variant="subtitle2" sx={{ mb: 1 }}>
                Active Players
              </Typography>
              <Typography
                variant="h1"
                sx={{ mb: 2, fontSize: { xs: '3rem', sm: '3.5rem' } }}
              >
                {activeNow.toLocaleString()}
              </Typography>

              <Grid container spacing={1.5}>
                <Grid item xs={6}>
                  <Box>
                    <Typography variant="subtitle2" sx={{ mb: 1 }}>
                      Peak Today
                    </Typography>
                    <Typography variant="h3" sx={{ fontSize: '1.75rem' }}>
                      {peakToday.toLocaleString()}
                    </Typography>
                  </Box>
                </Grid>
                <Grid item xs={6}>
                  <Box>
                    <Typography variant="subtitle2" sx={{ mb: 1 }}>
                      All-Time Peak
                    </Typography>
                    <Typography variant="h3" sx={{ fontSize: '1.75rem' }}>
                      {peakAlltime.toLocaleString()}
                    </Typography>
                  </Box>
                </Grid>
              </Grid>
            </CardContent>
          </Card>

          <Grid container spacing={2} sx={{ mb: 2 }}>
            {[
              { label: 'Today', value: today },
              { label: 'This Week', value: week },
              { label: 'This Month', value: month },
              { label: 'All Time', value: alltime },
            ].map((stat) => (
              <Grid item xs={6} key={stat.label}>
                <Paper sx={{ p: 2 }}>
                  <Typography variant="subtitle2" sx={{ mb: 1 }}>
                    {stat.label}
                  </Typography>
                  <Typography
                    variant="h3"
                    sx={{ fontSize: '1.75rem', fontWeight: 600 }}
                  >
                    {stat.value.toLocaleString()}
                  </Typography>
                </Paper>
              </Grid>
            ))}
          </Grid>

          <Card sx={{ mb: 2 }}>
            <CardContent>
              <Typography variant="subtitle2" sx={{ mb: 2 }}>
                Launcher Versions
              </Typography>

              <Box sx={{ maxHeight: 200, overflowY: 'auto', mb: 2 }}>
                {versions.length > 0 ? (
                  versions.map((item, idx) => (
                    <Box
                      key={idx}
                      sx={{
                        display: 'flex',
                        justifyContent: 'space-between',
                        alignItems: 'center',
                        py: 1,
                        px: 0,
                        borderBottom:
                          idx < versions.length - 1
                            ? '1px solid #2c2c2e'
                            : 'none',
                      }}
                    >
                      <Typography sx={{ fontSize: '0.875rem' }}>
                        {item.version}
                      </Typography>
                      <Typography
                        sx={{ fontSize: '0.875rem', color: '#98989f' }}
                      >
                        {item.count}
                      </Typography>
                    </Box>
                  ))
                ) : (
                  <Typography variant="body2">No data</Typography>
                )}
              </Box>

              <Box sx={{ display: 'flex', alignItems: 'center', gap: 1 }}>
                <Box
                  sx={{
                    width: 8,
                    height: 8,
                    borderRadius: '50%',
                    backgroundColor: '#00ff00',
                    flexShrink: 0,
                  }}
                />
                <Typography
                  variant="body2"
                  sx={{ fontSize: '0.813rem', color: '#98989f' }}
                >
                  Realtime Sync Enabled
                </Typography>
              </Box>
            </CardContent>
          </Card>

          <Box sx={{ width: '100%', height: 120 }}>
            <canvas ref={canvasRef} style={{ width: '100%', height: '100%' }} />
          </Box>
        </Container>
      </Box>
    </ThemeProvider>
  );
}

export default HollowDashboard;
